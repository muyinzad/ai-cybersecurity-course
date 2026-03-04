# Module 8: AI Security Tools

## Overview

This module covers building and using AI security tools - from setting up a lab to comparing commercial platforms. Learn to build custom AI security solutions.

---

## 8.1 Setting Up AI Security Lab

### Lab Environment Setup

```python
class AISecurityLab:
    """Set up AI security lab"""
    
    def __init__(self):
        self.components = {}
    
    def setup(self):
        """Setup complete lab"""
        
        # 1. Virtual Machines
        self.setup_vms()
        
        # 2. Networks
        self.setup_networks()
        
        # 3. Tools
        self.install_tools()
        
        # 4. AI Environment
        self.setup_ai_environment()
    
    def setup_vms(self):
        """Setup virtual machines"""
        
        vms = {
            'attacker': {
                'os': 'Kali Linux',
                'ram': '4GB',
                'cpus': 2
            },
            'victim': {
                'os': 'Ubuntu',
                'ram': '2GB',
                'cpus': 1
            },
            'siem': {
                'os': 'Ubuntu Server',
                'ram': '8GB',
                'cpus': 4
            }
        }
        
        for name, config in vms.items():
            print(f"Setting up {name} VM...")
            # VM creation code
    
    def setup_networks(self):
        """Setup networks"""
        
        networks = {
            'attacker_network': '192.168.100.0/24',
            'victim_network': '192.168.200.0/24',
            'management_network': '10.0.0.0/24'
        }
        
        return networks
    
    def install_tools(self):
        """Install security tools"""
        
        tools = [
            'nmap',
            'metasploit',
            'wireshark',
            'snort',
            'suricata'
        ]
        
        for tool in tools:
            print(f"Installing {tool}...")
            # Installation code
    
    def setup_ai_environment(self):
        """Setup AI environment"""
        
        requirements = {
            'python': '3.9+',
            'packages': [
                'tensorflow',
                'pytorch',
                'scikit-learn',
                'numpy',
                'pandas'
            ]
        }
        
        return requirements
```

### Docker Setup

```python
# docker-compose.yml for AI Security Lab
version: '3.8'

services:
  jupyter:
    image: jupyter/tensorflow-notebook
    ports:
      - "8888:8888"
    volumes:
      - ./notebooks:/home/jovyan/work
  
  siem:
    image: ossec/siem
    ports:
      - "1514:1514/udp"
  
  malware-sandbox:
    image: cuckoo/cuckoo
    ports:
      - "8000:8000"
```

---

## 8.2 Open-Source AI Tools

### Essential Open-Source Tools

```python
class OpenSourceTools:
    """Open-source AI security tools"""
    
    TOOLS = {
        # Threat Detection
        'moloch': 'Network analyzer',
        'zeek': 'Network security monitor',
        'suricata': 'IDS/IPS',
        'snort': 'IDS/IPS',
        
        # ML Security
        'cleverhans': 'Adversarial examples',
        'foolbox': 'Adversarial attacks',
        'art': 'Adversarial robustness',
        
        # SIEM
        'wazuh': 'SIEM',
        'security onion': 'SIEM',
        
        # Malware Analysis
        'cuckoo': 'Malware sandbox',
        'yara': 'Malware identification'
    }
    
    def install_tool(self, tool_name: str):
        """Install open-source tool"""
        
        if tool_name in self.TOOLS:
            print(f"Installing {tool_name}...")
            # Installation code
        else:
            print(f"Unknown tool: {tool_name}")
    
    def setup_tool(self, tool_name: str):
        """Setup and configure tool"""
        
        configs = {
            'suricata': {
                'rules': '/etc/suricata/rules',
                'interfaces': ['eth0']
            },
            'wazuh': {
                'manager': 'localhost',
                'agents': []
            }
        }
        
        return configs.get(tool_name, {})
```

### Tool Installation Scripts

```python
# Install AI Security Tools
def install_ai_security_tools():
    """Install AI security tools"""
    
    commands = [
        # Python packages
        "pip install tensorflow pytorch scikit-learn",
        
        # Security tools
        "apt-get install -y nmap wireshark",
        
        # ML security
        "pip install cleverhans foolbox adversarial-robustness-toolbox",
        
        # SIEM
        "wget https://packages.wazuh.com/4.x/apt key"
    ]
    
    for cmd in commands:
        print(f"Running: {cmd}")
        # Execute command
```

---

## 8.3 Commercial AI Platforms

### Platform Comparisons

```python
class CommercialPlatforms:
    """Commercial AI security platforms"""
    
    PLATFORMS = {
        'IBM Watson for Cyber Security': {
            'type': 'AI SIEM',
            'features': [
                'Watson AI integration',
                'Threat intelligence',
                'Automated response'
            ],
            'pricing': 'Enterprise',
            'deployment': 'Cloud'
        },
        
        'Darktrace': {
            'type': 'AI NDR',
            'features': [
                'Antigena AI',
                'Real-time detection',
                'Autonomous response'
            ],
            'pricing': 'Enterprise',
            'deployment': 'Cloud/Hybrid'
        },
        
        'Splunk Enterprise Security': {
            'type': 'SIEM',
            'features': [
                'ML-based analytics',
                'UEBA',
                'Custom dashboards'
            ],
            'pricing': '$150k+/year',
            'deployment': 'Cloud/On-prem'
        },
        
        'Microsoft Sentinel': {
            'type': 'SIEM',
            'features': [
                'Azure AI',
                'Cloud-native',
                'Cost-effective'
            ],
            'pricing': 'Pay per GB',
            'deployment': 'Cloud'
        }
    }
    
    def compare(self, platforms: list = None) -> pd.DataFrame:
        """Compare platforms"""
        
        if platforms is None:
            platforms = list(self.PLATFORMS.keys())
        
        data = []
        for name in platforms:
            if name in self.PLATFORMS:
                info = self.PLATFORMS[name]
                data.append({
                    'Platform': name,
                    'Type': info['type'],
                    'Deployment': info['deployment'],
                    'Pricing': info['pricing']
                })
        
        return pd.DataFrame(data)
    
    def recommend(self, requirements: Dict) -> list:
        """Recommend platform based on requirements"""
        
        recommendations = []
        
        if requirements.get('budget') == 'low':
            recommendations.append('Microsoft Sentinel')
        
        if requirements.get('scale') == 'large':
            recommendations.append('IBM Watson')
        
        if requirements.get('cloud_native'):
            recommendations.append('Azure Sentinel')
        
        return recommendations
```

---

## 8.4 Building Custom AI Tools

### Custom Tool Development

```python
class CustomAISecurityTool:
    """Build custom AI security tool"""
    
    def __init__(self):
        self.model = None
        self.config = self.load_config()
    
    def build(self):
        """Build AI security tool"""
        
        # 1. Define problem
        problem = self.define_problem()
        
        # 2. Collect data
        data = self.collect_data()
        
        # 3. Preprocess
        processed = self.preprocess(data)
        
        # 4. Train model
        self.model = self.train(processed)
        
        # 5. Deploy
        self.deploy()
        
        return self.model
    
    def define_problem(self) -> Dict:
        """Define the security problem"""
        
        return {
            'type': 'classification',
            'task': 'malware_detection',
            'input': 'file_features',
            'output': 'malicious/benign'
        }
    
    def collect_data(self) -> pd.DataFrame:
        """Collect training data"""
        
        # Load malware samples
        malware = self.load_malware_samples()
        
        # Load benign samples
        benign = self.load_benign_samples()
        
        # Combine
        data = pd.concat([malware, benign])
        
        return data
    
    def preprocess(self, data: pd.DataFrame) -> np.array:
        """Preprocess data"""
        
        # Feature extraction
        features = self.extract_features(data)
        
        # Normalize
        normalized = self.normalize(features)
        
        return normalized
    
    def train(self, data) -> object:
        """Train the model"""
        
        model = RandomForestClassifier(n_estimators=100)
        model.fit(data['features'], data['labels'])
        
        return model
    
    def deploy(self):
        """Deploy the model"""
        
        # Save model
        import joblib
        joblib.dump(self.model, 'malware_detector.pkl')
        
        # Create API
        self.create_api()
    
    def create_api(self):
        """Create prediction API"""
        
        from flask import Flask, request, jsonify
        import joblib
        
        app = Flask(__name__)
        model = joblib.load('malware_detector.pkl')
        
        @app.route('/predict', methods=['POST'])
        def predict():
            data = request.json
            features = data['features']
            prediction = model.predict([features])
            
            return jsonify({
                'prediction': prediction[0],
                'confidence': max(model.predict_proba([features])[0])
            })
        
        return app
```

### Complete Example Tool

```python
# threat_detector.py
class ThreatDetector:
    """Complete threat detection tool"""
    
    def __init__(self):
        self.model = self.load_model()
        self.features = FeatureExtractor()
    
    def detect(self, data) -> Dict:
        """Detect threats"""
        
        # Extract features
        features = self.features.extract(data)
        
        # Predict
        prediction = self.model.predict([features])
        probability = self.model.predict_proba([features])
        
        return {
            'is_threat': bool(prediction[0]),
            'confidence': max(probability[0]),
            'threat_type': self.get_threat_type(prediction[0]),
            'severity': self.calculate_severity(probability[0])
        }
    
    def get_threat_type(self, prediction):
        """Get threat type"""
        
        types = {
            0: 'benign',
            1: 'malware',
            2: 'phishing',
            3: 'exploit'
        }
        
        return types.get(prediction, 'unknown')
```

---

## 8.5 Integrating AI into Workflows

### Workflow Integration

```python
class AIWorkflowIntegration:
    """Integrate AI into security workflows"""
    
    def __init__(self):
        self.tools = {}
        self.ai_models = {}
    
    def integrate_with_siem(self, siem_type: str):
        """Integrate with SIEM"""
        
        if siem_type == 'splunk':
            return SplunkIntegration()
        elif siem_type == 'elastic':
            return ElasticIntegration()
    
    def integrate_with_firewall(self, firewall: str):
        """Integrate with firewall"""
        
        return FirewallIntegration(firewall)
    
    def integrate_with_edr(self, edr: str):
        """Integrate with EDR"""
        
        return EDRIntegration(edr)
    
    def create_pipeline(self) -> Dict:
        """Create AI processing pipeline"""
        
        return {
            'input': 'logs',
            'stages': [
                {'name': 'preprocess', 'tool': 'normalizer'},
                {'name': 'detect', 'tool': 'ai_model'},
                {'name': 'respond', 'tool': 'automation'}
            ],
            'output': 'alerts'
        }
```

### Complete Integration Example

```python
# Example: Integrate AI Detection with Firewall Block
class SecurityPipeline:
    """Complete security pipeline"""
    
    def __init__(self):
        self.detector = ThreatDetector()
        self.firewall = FirewallAPI()
        self.logger = AlertLogger()
    
    def process_event(self, event: Dict):
        """Process security event"""
        
        # Detect threat
        detection = self.detector.detect(event)
        
        if detection['is_threat'] and detection['confidence'] > 0.9:
            # Block malicious IP
            self.firewall.block_ip(event['source_ip'])
            
            # Log alert
            self.logger.log({
                'event': 'threat_blocked',
                'source': event['source_ip'],
                'threat': detection['threat_type'],
                'confidence': detection['confidence']
            })
            
            # Notify
            self.notify(event)
    
    def notify(self, event: Dict):
        """Send notifications"""
        
        message = f"Blocked malicious IP: {event['source_ip']}"
        
        # Send to Slack
        slack.notify(message)
        
        # Send email
        email.alert(message)
```

---

## 8.6 Tool Comparisons

### AI Security Tool Comparison

```python
def compare_tools():
    """Compare AI security tools"""
    
    comparison = {
        'Threat Detection': {
            'Darktrace': {'accuracy': 0.95, 'speed': 'fast', 'cost': 'high'},
            'Microsoft Sentinel': {'accuracy': 0.88, 'speed': 'fast', 'cost': 'medium'},
            'Custom Model': {'accuracy': 0.90, 'speed': 'fast', 'cost': 'low'}
        },
        
        'Malware Detection': {
            'YARA': {'accuracy': 0.85, 'speed': 'fast', 'cost': 'free'},
            'ClamAV': {'accuracy': 0.70, 'speed': 'fast', 'cost': 'free'},
            'Custom ML': {'accuracy': 0.95, 'speed': 'medium', 'cost': 'medium'}
        },
        
        'SIEM': {
            'Splunk': {'features': 10, 'scalability': 'high', 'cost': 'high'},
            'Wazuh': {'features': 8, 'scalability': 'medium', 'cost': 'free'},
            'Elastic': {'features': 9, 'scalability': 'high', 'cost': 'medium'}
        }
    }
    
    return comparison
```

### Selection Criteria

| Criteria | Weight | Questions |
|----------|--------|-----------|
| Accuracy | High | Does it detect threats reliably? |
| Speed | Medium | Real-time processing? |
| Cost | Medium | Within budget? |
| Integration | High | Works with existing tools? |
| Scalability | Medium | Handles growth? |
| Support | Low | Vendor support available? |

---

## 8.7 Hands-On Lab

### Lab 8.1: Build Complete Detection Tool

```python
class CompleteDetectionTool:
    """Build complete detection tool"""
    
    def __init__(self):
        self.model = None
        self.config = {}
    
    def build(self, data_path: str):
        """Build detection tool"""
        
        # Load data
        data = pd.read_csv(data_path)
        
        # Preprocess
        X, y = self.preprocess(data)
        
        # Train
        self.model = RandomForestClassifier(n_estimators=100)
        self.model.fit(X, y)
        
        # Save
        self.save()
        
        return self.model
    
    def preprocess(self, data):
        """Preprocess data"""
        
        # Features
        X = data.drop('label', axis=1)
        
        # Labels
        y = data['label']
        
        return X, y
    
    def save(self):
        """Save model"""
        
        import joblib
        joblib.dump(self.model, 'detector.pkl')
    
    def load(self):
        """Load model"""
        
        import joblib
        self.model = joblib.load('detector.pkl')
    
    def predict(self, features):
        """Make prediction"""
        
        return self.model.predict(features)
```

### Lab 8.2: Create API Service

```python
# Create API for detection tool
def create_detection_api():
    """Create API service"""
    
    from flask import Flask, request, jsonify
    import joblib
    
    app = Flask(__name__)
    model = joblib.load('detector.pkl')
    
    @app.route('/detect', methods=['POST'])
    def detect():
        data = request.json
        features = data['features']
        
        prediction = model.predict([features])[0]
        probability = max(model.predict_proba([features])[0])
        
        return jsonify({
            'prediction': 'malicious' if prediction else 'benign',
            'confidence': probability
        })
    
    app.run(port=5000)
```

---

## Module 8 Summary

### Key Takeaways

1. **Lab setup** is essential for AI security work
2. **Open-source tools** provide strong foundation
3. **Commercial platforms** offer enterprise features
4. **Custom tools** can be built for specific needs
5. **Integration** is key to effective security

### Tool Categories

| Category | Tools |
|----------|-------|
| Detection | Darktrace, Microsoft Sentinel |
| SIEM | Splunk, Wazuh, Elastic |
| ML Security | CleverHans, ART, Foolbox |
| Malware | Cuckoo, YARA, ClamAV |

### Course Summary

This course covered:
- ✅ AI fundamentals for security
- ✅ Python for AI security
- ✅ Threat detection with AI
- ✅ AI-powered reconnaissance
- ✅ AI exploitation tools
- ✅ AI for penetration testing
- ✅ AI in SOC & incident response
- ✅ Building AI security tools

### Next Steps

1. **Practice** with lab environments
2. **Build** custom tools
3. **Contribute** to open source
4. **Stay updated** with AI security research

---

## Quick Reference

```python
# Quick start
pip install tensorflow pytorch scikit-learn
pip install cleverhans foolbox adversarial-robustness-toolbox
```
