# loops

This feeds a while loop with the output of a grep command:

```bash
count=0
while IFS=":" read -r user _; do 
  
  # "$user" holds the username in /etc/passwd 
  ((count++))

done < <(grep "hello" /etc/passwd)
```

In this way variable count is useable after the loop too because the while loop is not used in a subshell.
