```python
import json
import pandas as pd
from datetime import datetime
from collections import defaultdict


with open('input.txt', 'r') as f:
    commits = json.load(f)
    
changes = []
for record in commits:
    for file in record['files']:
        change = {
            'username': record['username'], 
            'commit_time': datetime.strptime(record['commit_time'], '%Y/%m/%d %H:%M:%S'),
            'filename': file['name'],
            'changed_lines': file['changed_lines']
        }
        changes.append(change)

changes = sorted(changes, key=lambda change: change['commit_time'])

user_commits = defaultdict(int)
for record in commits:
    user_commits[record['username']] += 1
    
user_changed_lines = defaultdict(int)
for change in changes:
    user_changed_lines[change['username']] += change['changed_lines']
    
user_new_files = defaultdict(int)
files = set()
for change in changes:
    if change['filename'] not in files:
        files.add(change['filename'])
        user_new_files[change['username']] += 1
        
commits_series = pd.Series(user_commits)
changed_lines_series = pd.Series(user_changed_lines)
new_files_series = pd.Series(user_new_files)

df = pd.DataFrame({
    'commits':commits_series, 
    'changed_lines': changed_lines_series, 
    'new_files': new_files_series
})
df.sort_index(inplace=True)
df = df.rename_axis('username').reset_index()

print(df.to_string(index=False))
```
