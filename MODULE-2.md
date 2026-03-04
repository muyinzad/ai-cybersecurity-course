# Module 2: Python for AI Security

## Overview

This module covers Python programming essentials for building AI-powered security tools. Master the libraries and frameworks used in AI cybersecurity applications.

---

## 2.1 Python Basics Review

### Core Concepts for Security

```python
# Variables and Data Types
username = "admin"
user_id = 12345
is_active = True
ip_addresses = ["192.168.1.1", "10.0.0.1"]

# Control Flow
def check_security(user):
    if user.is_active and user.permission_level > 5:
        return "granted"
    elif user.is_active:
        return "limited"
    return "denied"

# Error Handling
def safe_execute(code):
    try:
        result = eval(code)
        return result
    except SyntaxError as e:
        log_security_event(f"Syntax error: {e}")
        return None
    except Exception as e:
        log_security_event(f"Unexpected error: {e}")
        return None
```

---

## 2.2 NumPy for Security Data

### Numerical Computing

```python
import numpy as np

class NetworkAnalyzer:
    """Analyze network traffic with NumPy"""
    
    def __init__(self):
        self.packet_sizes = np.array([])
        self.timestamps = np.array([])
    
    def add_packet(self, size, timestamp):
        """Add packet data"""
        self.packet_sizes = np.append(self.packet_sizes, size)
        self.timestamps = np.append(self.timestamps, timestamp)
    
    def detect_anomalies(self, threshold=2.0):
        """Detect anomalous packet sizes"""
        mean = np.mean(self.packet_sizes)
        std = np.std(self.packet_sizes)
        
        # Z-score analysis
        z_scores = np.abs((self.packet_sizes - mean) / std)
        
        # Return indices of anomalies
        return np.where(z_scores > threshold)[0]
    
    def calculate_bandwidth(self):
        """Calculate bandwidth statistics"""
        if len(self.timestamps) < 2:
            return 0
        
        time_diffs = np.diff(self.timestamps)
        bandwidth = self.packet_sizes[1:] / time_diffs
        
        return {
            'mean': np.mean(bandwidth),
            'max': np.max(bandwidth),
            'min': np.min(bandwidth),
            'std': np.std(bandwidth)
        }
```

### Packet Analysis Example

```python
def analyze_packets(packet_sizes):
    """Analyze packet size distribution"""
    sizes = np.array(packet_sizes)
    
    return {
        'total': len(sizes),
        'mean_size': np.mean(sizes),
        'median_size': np.median(sizes),
        'std_dev': np.std(sizes),
        'min': np.min(sizes),
        'max': np.max(sizes),
        'percentiles': {
            '25': np.percentile(sizes, 25),
            '50': np.percentile(sizes, 50),
            '75': np.percentile(sizes, 75),
            '95': np.percentile(sizes, 95),
            '99': np.percentile(sizes, 99)
        }
    }
```

---

## 2.3 Pandas for Security Data

### Data Analysis

```python
import pandas as pd
from datetime import datetime

class SecurityEventLogger:
    """Log and analyze security events"""
    
    def __init__(self):
        self.events = pd.DataFrame(columns=[
            'timestamp', 'event_type', 'source_ip', 
            'dest_ip', 'severity', 'description'
        ])
    
    def log_event(self, event_type, source_ip, dest_ip, 
                  severity, description):
        """Log a security event"""
        new_event = pd.DataFrame([{
            'timestamp': datetime.now(),
            'event_type': event_type,
            'source_ip': source_ip,
            'dest_ip': dest_ip,
            'severity': severity,
            'description': description
        }])
        
        self.events = pd.concat([self.events, new_event], ignore_index=True)
    
    def get_attack_summary(self):
        """Get summary of attacks"""
        return self.events.groupby('event_type').size().sort_values(ascending=False)
    
    def get_top_attackers(self):
        """Get top attacking IPs"""
        return self.events.groupby('source_ip').size().sort_values(ascending=False).head(10)
    
    def get_severity_distribution(self):
        """Get distribution by severity"""
        return self.events.groupby('severity').size()
    
    def time_analysis(self, time_window='1H'):
        """Analyze events over time"""
        self.events.set_index('timestamp')
        return self.events.resample(time_window).size()
```

### Malware Analysis with Pandas

```python
class MalwareAnalyzer:
    """Analyze malware samples with Pandas"""
    
    def __init__(self, samples_data):
        self.df = pd.DataFrame(samples_data)
    
    def classify_by_size(self):
        """Classify samples by file size"""
        return self.df.groupby(
            pd.cut(self.df['file_size'], bins=[0, 10000, 100000, 1000000, np.inf],
                   labels=['tiny', 'small', 'medium', 'large'])
        ).size()
    
    def detect_outliers(self):
        """Detect outlier samples"""
        Q1 = self.df['entropy'].quantile(0.25)
        Q3 = self.df['entropy'].quantile(0.75)
        IQR = Q3 - Q1
        
        outliers = self.df[
            (self.df['entropy'] < Q1 - 1.5 * IQR) |
            (self.df['entropy'] > Q3 + 1.5 * IQR)
        ]
        
        return outliers
    
    def correlate_features(self):
        """Find feature correlations"""
        numeric_cols = self.df.select_dtypes(include=[np.number]).columns
        return self.df[numeric_cols].corr()
```

---

## 2.4 Scikit-learn Fundamentals

### Machine Learning Basics

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import classification_report, confusion_matrix

class ThreatDetector:
    """Detect threats using machine learning"""
    
    def __init__(self):
        self.model = RandomForestClassifier(n_estimators=100)
        self.scaler = StandardScaler()
        self.is_trained = False
    
    def prepare_data(self, features, labels):
        """Prepare training data"""
        # Scale features
        scaled_features = self.scaler.fit_transform(features)
        
        # Split data
        X_train, X_test, y_train, y_test = train_test_split(
            scaled_features, labels, test_size=0.2, random_state=42
        )
        
        return X_train, X_test, y_train, y_test
    
    def train(self, features, labels):
        """Train the model"""
        X_train, X_test, y_train, y_test = self.prepare_data(features, labels)
        
        self.model.fit(X_train, y_train)
        self.is_trained = True
        
        # Evaluate
        predictions = self.model.predict(X_test)
        
        return {
            'accuracy': self.model.score(X_test, y_test),
            'report': classification_report(y_test, predictions),
            'confusion_matrix': confusion_matrix(y_test, predictions)
        }
    
    def predict(self, features):
        """Predict threat"""
        if not self.is_trained:
            raise ValueError("Model not trained")
        
        scaled = self.scaler.transform(features)
        prediction = self.model.predict(scaled)
        probability = self.model.predict_proba(scaled)
        
        return {
            'prediction': prediction[0],
            'confidence': max(probability[0]),
            'probabilities': dict(zip(self.model.classes_, probability[0]))
        }
```

### Anomaly Detection

```python
from sklearn.ensemble import IsolationForest

class AnomalyDetector:
    """Detect anomalies using Isolation Forest"""
    
    def __init__(self, contamination=0.1):
        self.model = IsolationForest(
            contamination=contamination,
            random_state=42
        )
        self.is_fitted = False
    
    def fit(self, normal_data):
        """Fit on normal data"""
        self.model.fit(normal_data)
        self.is_fitted = True
    
    def detect(self, data):
        """Detect anomalies"""
        if not self.is_fitted:
            raise ValueError("Model not fitted")
        
        predictions = self.model.predict(data)
        scores = self.model.decision_function(data)
        
        return {
            'predictions': predictions,
            'scores': scores,
            'anomalies': np.where(predictions == -1)[0]
        }
```

---

## 2.5 TensorFlow/PyTorch Basics

### Neural Networks for Security

```python
import torch
import torch.nn as nn
import torch.optim as optim

class PhishingDetector(nn.Module):
    """Neural network for phishing detection"""
    
    def __init__(self, input_size):
        super(PhishingDetector, self).__init__()
        
        self.network = nn.Sequential(
            nn.Linear(input_size, 128),
            nn.ReLU(),
            nn.Dropout(0.3),
            nn.Linear(128, 64),
            nn.ReLU(),
            nn.Dropout(0.3),
            nn.Linear(64, 32),
            nn.ReLU(),
            nn.Linear(32, 2),  # Binary classification
            nn.Softmax(dim=1)
        )
    
    def forward(self, x):
        return self.network(x)

def train_phishing_model(train_data, train_labels, epochs=10):
    """Train phishing detection model"""
    
    model = PhishingDetector(input_size=train_data.shape[1])
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.Adam(model.parameters(), lr=0.001)
    
    for epoch in range(epochs):
        optimizer.zero_grad()
        outputs = model(train_data)
        loss = criterion(outputs, train_labels)
        loss.backward()
        optimizer.step()
        
        if (epoch + 1) % 2 == 0:
            print(f"Epoch {epoch+1}, Loss: {loss.item():.4f}")
    
    return model
```

### TensorFlow Example

```python
import tensorflow as tf
from tensorflow import keras

def build_malware_classifier(input_dim):
    """Build malware classification model"""
    
    model = keras.Sequential([
        keras.layers.Dense(256, activation='relu', input_shape=(input_dim,)),
        keras.layers.Dropout(0.4),
        keras.layers.Dense(128, activation='relu'),
        keras.layers.Dropout(0.4),
        keras.layers.Dense(64, activation='relu'),
        keras.layers.Dense(2, activation='softmax')
    ])
    
    model.compile(
        optimizer='adam',
        loss='sparse_categorical_crossentropy',
        metrics=['accuracy']
    )
    
    return model

def train_malware_model(train_data, train_labels, epochs=20):
    """Train malware classifier"""
    
    model = build_malware_classifier(train_data.shape[1])
    
    history = model.fit(
        train_data, train_labels,
        epochs=epochs,
        validation_split=0.2,
        batch_size=32
    )
    
    return model, history
```

---

## 2.6 Building ML Models for Security

### Complete Example: Intrusion Detection

```python
class IntrusionDetectionSystem:
    """Complete intrusion detection system"""
    
    def __init__(self):
        self.model = None
        self.scaler = StandardScaler()
        self.label_encoder = None
    
    def preprocess_data(self, raw_data):
        """Preprocess network data"""
        
        # Handle categorical features
        categorical_cols = ['protocol', 'service', 'flag']
        numeric_cols = ['duration', 'src_bytes', 'dst_bytes']
        
        # One-hot encode categoricals
        processed = pd.get_dummies(raw_data, columns=categorical_cols)
        
        # Scale numericals
        processed[numeric_cols] = self.scaler.fit_transform(processed[numeric_cols])
        
        return processed
    
    def train(self, data, labels):
        """Train detection model"""
        
        # Preprocess
        processed_data = self.preprocess_data(data)
        
        # Split
        X_train, X_test, y_train, y_test = train_test_split(
            processed_data, labels, test_size=0.2, random_state=42
        )
        
        # Train Random Forest
        self.model = RandomForestClassifier(n_estimators=100, max_depth=20)
        self.model.fit(X_train, y_train)
        
        # Evaluate
        accuracy = self.model.score(X_test, y_test)
        
        return {'accuracy': accuracy}
    
    def detect(self, network_packet):
        """Detect if packet is attack"""
        
        # Preprocess
        processed = self.preprocess_data([network_packet])
        
        # Predict
        prediction = self.model.predict(processed)
        probability = self.model.predict_proba(processed)
        
        return {
            'is_attack': bool(prediction[0]),
            'confidence': max(probability[0]),
            'attack_type': self.model.classes_[prediction[0]]
        }
```

---

## 2.7 Hands-On Lab

### Lab 2.1: Build a Simple Threat Detector

```python
class SimpleThreatDetector:
    """Build a basic threat detector"""
    
    def __init__(self):
        self.features = []
        self.labels = []
        self.model = None
    
    def add_sample(self, features, is_threat):
        """Add training sample"""
        self.features.append(features)
        self.labels.append(1 if is_threat else 0)
    
    def train(self):
        """Train the model"""
        X = np.array(self.features)
        y = np.array(self.labels)
        
        self.model = RandomForestClassifier(n_estimators=50)
        self.model.fit(X, y)
    
    def predict(self, features):
        """Predict threat level"""
        if self.model is None:
            raise ValueError("Model not trained")
        
        prediction = self.model.predict([features])
        probability = self.model.predict_proba([features])
        
        return {
            'is_threat': bool(prediction[0]),
            'confidence': max(probability[0])
        }
```

---

## Module 2 Summary

### Key Takeaways

1. **NumPy** enables fast numerical analysis for security data
2. **Pandas** provides powerful data manipulation for event logs
3. **Scikit-learn** offers practical ML for threat detection
4. **PyTorch/TensorFlow** enable deep learning for complex detection

### Libraries Overview

| Library | Purpose | Use Case |
|---------|---------|----------|
| NumPy | Numerical computing | Packet analysis |
| Pandas | Data manipulation | Log analysis |
| Scikit-learn | ML algorithms | Threat detection |
| PyTorch | Deep learning | Complex patterns |
| TensorFlow | Deep learning | Production models |

### Next Steps

Proceed to **Module 3: Threat Detection with AI** to build detection systems.

---

## Quick Reference

```python
# Quick imports
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
import torch
import tensorflow as tf
```
