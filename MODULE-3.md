# 🤖 AI Cybersecurity Course - Module 3
## Threat Detection with AI

---

## 3.1 Anomaly Detection Systems

### What is Anomaly Detection?
Finding patterns in data that don't match normal behavior.

```
Normal Behavior:
├── Regular login times
├── Expected network traffic
├── Typical file access
└── Standard command patterns

Anomalies:
├── Unusual login times
├── Unexpected data transfer
├── Abnormal file access
└── Strange command execution
```

---

### Building Anomaly Detector

```python
import numpy as np
from sklearn.ensemble import IsolationForest
from sklearn.preprocessing import StandardScaler

# Sample network data (features)
# [bytes_sent, bytes_received, connections, duration]
normal_traffic = np.array([
    [1000, 2000, 5, 60],
    [1200, 1800, 4, 55],
    [1100, 1900, 5, 58],
    # ... thousands of normal samples
])

# Train Isolation Forest
scaler = StandardScaler()
X_scaled = scaler.fit_transform(normal_traffic)

model = IsolationForest(contamination=0.1, random_state=42)
model.fit(X_scaled)

# Detect anomalies in new traffic
new_traffic = np.array([[50000, 100, 200, 10]])
new_scaled = scaler.transform(new_traffic)

prediction = model.predict(new_scaled)
# -1 = anomaly, 1 = normal

if prediction == -1:
    print("⚠️ ANOMALY DETECTED!")
```

---

## 3.2 Malware Classification with ML

### Feature Extraction

```python
import pefile
import numpy as np

def extract_pe_features(file_path):
    """Extract features from PE file"""
    try:
        pe = pefile.PE(file_path)
        
        features = {
            # Entry point
            'entry_point': pe.OPTIONAL_HEADER.AddressOfEntryPoint,
            
            # Sections
            'num_sections': len(pe.sections),
            
            # Sizes
            'size_of_code': pe.OPTIONAL_HEADER.SizeOfCode,
            'size_of_image': pe.OPTIONAL_HEADER.SizeOfImage,
            
            # Entropy
            'entropy': calculate_entropy(pe),
            
            # Imports/Exports
            'num_imports': len(pe.DIRECTORY_ENTRY_IMPORT) if hasattr(pe, 'DIRECTORY_ENTRY_IMPORT') else 0,
            'num_exports': len(pe.DIRECTORY_ENTRY_EXPORT) if hasattr(pe, 'DIRECTORY_ENTRY_EXPORT') else 0,
            
            # Resources
            'has_resources': hasattr(pe, 'DIRECTORY_ENTRY_RESOURCE'),
        }
        
        return features
    except:
        return None

def calculate_entropy(pe):
    """Calculate section entropy"""
    import math
    # Entropy calculation code
    return 0.0
```

### ML Malware Classifier

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
import joblib

# Load dataset (malware vs benign)
X, y = load_malware_dataset()  # Your dataset

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Train model
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)

# Evaluate
accuracy = model.score(X_test, y_test)
print(f"Model Accuracy: {accuracy * 100}%")

# Save model
joblib.dump(model, 'malware_classifier.pkl')
```

---

## 3.3 Network Intrusion Detection

### Network Traffic Features

```python
# Features for network IDS
features = [
    'duration',           # Length of connection
    'protocol_type',      # TCP, UDP, ICMP
    'service',            # http, ftp, smtp, etc.
    'src_bytes',          # Source bytes
    'dst_bytes',          # Destination bytes
    'count',              # Connections to same host
    'serror_rate',       # SYN errors
    'rerror_rate',        # Reject errors
    'same_srv_rate',     # Same service rate
    'diff_srv_rate',     # Different service rate
]
```

### Building Network IDS

```python
from sklearn.neural_network import MLPClassifier
from sklearn.preprocessing import LabelEncoder

def build_network_ids():
    # Load KDD Cup 99 or NSL-KDD dataset
    X, y = load_network_data()
    
    # Encode categorical features
    le = LabelEncoder()
    y_encoded = le.fit_transform(y)
    
    # Split
    X_train, X_test, y_train, y_test = train_test_split(
        X, y_encoded, test_size=0.2
    )
    
    # Neural Network Classifier
    model = MLPClassifier(
        hidden_layer_sizes=(64, 32),
        activation='relu',
        max_iter=500
    )
    
    model.fit(X_train, y_train)
    
    # Test
    accuracy = model.score(X_test, y_test)
    print(f"Network IDS Accuracy: {accuracy * 100}%")
    
    return model, le
```

---

## 3.4 Phishing Detection

### URL Features

```python
def extract_url_features(url):
    """Extract features from URL"""
    from urllib.parse import urlparse
    
    parsed = urlparse(url)
    
    features = {
        # Length features
        'url_length': len(url),
        'num_dots': url.count('.'),
        'num_hyphens': url.count('-'),
        'num_underscores': url.count('_'),
        'num_slashes': url.count('/'),
        
        # Special characters
        'has_https': 1 if parsed.scheme == 'https' else 0,
        'has_ip': 1 if is_ip_address(parsed.netloc) else 0,
        
        # Domain features
        'domain_length': len(parsed.netloc),
        'subdomain_depth': parsed.netloc.count('.') - 1,
        
        # Suspicious patterns
        'has_at_symbol': 1 if '@' in url else 0,
        'has_double_slash': 1 if '//' in parsed.path else 0,
        'has_port': 1 if ':' in parsed.netloc else 0,
        
        # Known phishing keywords
        'has_login': 1 if 'login' in url.lower() else 0,
        'has_secure': 1 if 'secure' in url.lower() else 0,
        'has_account': 1 if 'account' in url.lower() else 0,
    }
    
    return features
```

### Phishing Classifier

```python
from sklearn.linear_model import LogisticRegression
from sklearn.feature_extraction import DictVectorizer

def train_phishing_detector():
    # Training data: list of (url_features, label)
    data = [
        ({'url_length': 50, 'has_https': 1, ...}, 'legitimate'),
        ({'url_length': 150, 'has_https': 0, ...}, 'phishing'),
        # ... more samples
    ]
    
    X = [d[0] for d in data]
    y = [d[1] for d in data]
    
    # Vectorize
    vec = DictVectorizer()
    X_vec = vec.fit_transform(X)
    
    # Train
    model = LogisticRegression()
    model.fit(X_vec, y)
    
    return model, vec
```

---

## 3.5 User Behavior Analytics (UBA)

### Tracking User Behavior

```python
class UserBehaviorTracker:
    def __init__(self, user_id):
        self.user_id = user_id
        self.login_times = []
        self.ips = set()
        self.files_accessed = []
        self.commands = []
        
    def add_login(self, timestamp, ip):
        self.login_times.append(timestamp)
        self.ips.add(ip)
        
    def add_file_access(self, filename):
        self.files_accessed.append(filename)
        
    def is_anomalous(self, timestamp, ip, action):
        # Check unusual login time
        if self.login_times:
            avg_time = np.mean([t.hour for t in self.login_times])
            if abs(timestamp.hour - avg_time) > 3:
                return True, "Unusual login time"
        
        # Check new IP
        if ip not in self.ips:
            return True, "New IP address"
            
        return False, "Normal"
```

---

## 3.6 Complete Detection Pipeline

```python
class AISecurityPipeline:
    def __init__(self):
        self.network_model = load_model('network_ids.pkl')
        self.malware_model = load_model('malware_classifier.pkl')
        self.phishing_model = load_model('phishing_detector.pkl')
        
    def analyze_network_traffic(self, packet):
        features = extract_network_features(packet)
        prediction = self.network_model.predict([features])
        return prediction
    
    def analyze_file(self, file_path):
        features = extract_pe_features(file_path)
        prediction = self.malware_model.predict([features])
        return prediction
    
    def analyze_url(self, url):
        features = extract_url_features(url)
        prediction = self.phishing_model.predict([features])
        return prediction
    
    def full_scan(self, target):
        results = {
            'network': self.analyze_network_traffic(target),
            'malware': self.analyze_file(target) if is_file(target) else None,
            'url': self.analyze_url(target) if is_url(target) else None,
        }
        return results
```

---

## Key Takeaways

✅ Anomaly detection finds unknown threats
✅ ML can classify malware with high accuracy
✅ Network IDS can detect intrusions
✅ Phishing detection is effective with ML
✅ UBA catches insider threats

---

*Module 3 Complete! Next: AI-Powered Reconnaissance 🤖*
