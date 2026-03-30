```bash
docker run -it --name bash-lab ubuntu:24.04 bash
```
```bash
apt update && apt install -y \
  curl \
  wget \
  iputils-ping \
  net-tools \
  iproute2 \
  procps \
  psmisc \
  dnsutils \
  traceroute \
  vim \
  nano \
  less \
  grep \
  findutils \
  sed \
  gawk \
  tar \
  gzip
```
```bash
docker start -ai bash-lab
```

### Create Multiple Folders
```bash
mkdir -p /workspace/project/{logs,configs,scripts,data}
```

### Find Directories
```bash
find . -type d
```
### Create and Echo
```bash
echo "sinan" > text.txt
echo "merhaba" >> text.txt
```

### Follow only new lines
```bash
tail -n 0 -f app.log
```

### heredoc and grep
```bash
# Take everyhng until EOF as input. send it to file
cat <<EOF >> /workspace/project/logs/app.log
2026-03-30 ERROR database connection failed
2026-03-30 INFO retrying connection
2026-03-30 WARNING high memory usage
2026-03-30 ERROR invalid credentials
EOF
```
```bash
grep ERROR logs/app.log
# case insensitive
grep -i warning log/app.log
# count the findings
grep -c ERROR log/app.log
```

### Redirect stout and sterr
```bash
ls /workspace/file-exist > output.txt 2> error.txt
# redirecting to same file
ls /workspace/file-exits > output.txt 2>&1
# silence errors
command 2>/dev/null
```