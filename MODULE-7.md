# Module 7: AI in SOC & Incident Response

## Overview

This module covers AI-powered Security Operations Center (SOC) functions and incident response automation. Learn to build AI-driven security operations.

---

## 7.1 AI-Powered SIEM

### Modern SIEM with AI

```python
class AISiem:
    """AI-powered SIEM system"""
    
    def __init__(self):
        self.data_sources = []
        self.ml_models = {}
        self.alert_engine = AlertEngine()
    
    def ingest_log(self, log_data: dict):
        """Ingest log data"""
        
        # Normalize data
        normalized = self.normalize(log_data)
        
        # AI analysis
        analysis = self.analyze(normalized)
        
        # Check alerts
        if analysis['is_threat']:
            self.alert_engine.create_alert(analysis)
        
        # Store
        self.store(normalized)
    
    def normalize(self, log_data: dict) -> dict:
        """Normalize log data"""
        
        return {
            'timestamp': log_data['timestamp'],
            'source_ip': log_data.get('src_ip'),
            'dest_ip': log_data.get('dst_ip'),
            'event_type': log_data.get('type'),
            'severity': log_data.get('severity'),
            'raw_data': log_data
        }
    
    def analyze(self, log_data: dict) -> dict:
        """AI analysis of log"""
        
        # Use multiple models
        anomaly_score = self.ml_models['anomaly'].predict(log_data)
        threat_score = self.ml_models['threat'].predict(log_data)
        
        is_threat = threat_score > 0.7
        
        return {
            'anomaly_score': anomaly_score,
            'threat_score': threat_score,
            'is_threat': is_threat,
            'recommendation': self.get_recommendation(threat_score)
        }
```

### SIEM Integration

```python
class SiemIntegrator:
    """Integrate AI with SIEM"""
    
    def __init__(self, siem_type='splunk'):
        self.siem_type = siem_type
        self.connectors = self.setup_connectors()
    
    def setup_connectors(self):
        """Setup data connectors"""
        
        return {
            'firewall': FirewallConnector(),
            'ids': IDSConnector(),
            'endpoint': EndpointConnector(),
            'cloud': CloudConnector()
        }
    
    def query(self, query: str) -> list:
        """Query SIEM"""
        
        if self.siem_type == 'splunk':
            return self.query_splunk(query)
        elif self.siem_type == 'elastic':
            return self.query_elastic(query)
    
    def query_splunk(self, query: str) -> list:
        """Query Splunk"""
        
        # Splunk API call
        return []
```

---

## 7.2 Automated Threat Hunting

### AI Threat Hunting

```python
class AIThreatHunter:
    """AI-powered threat hunting"""
    
    def __init__(self):
        self.hypothesis_generator = HypothesisGenerator()
        self.ml_model = self.load_detection_model()
        self.hunted_threats = []
    
    def hunt(self) -> List[Dict]:
        """Run threat hunting"""
        
        # Generate hypotheses
        hypotheses = self.hypothesis_generator.generate()
        
        # Test hypotheses
        results = []
        for hypothesis in hypotheses:
            result = self.test_hypothesis(hypothesis)
            if result['found']:
                results.append(result)
                self.hunted_threats.append(result)
        
        return results
    
    def test_hypothesis(self, hypothesis: Dict) -> Dict:
        """Test a hunting hypothesis"""
        
        # Build query
        query = self.build_query(hypothesis)
        
        # Execute
        data = self.execute_query(query)
        
        # Analyze
        analysis = self.ml_model.analyze(data)
        
        return {
            'hypothesis': hypothesis,
            'found': analysis['is_malicious'],
            'confidence': analysis['confidence'],
            'evidence': analysis['evidence']
        }
    
    def build_query(self, hypothesis: Dict) -> str:
        """Build SIEM query"""
        
        return f"""
        index=* 
        | where 
            src_ip={hypothesis['indicator']}
            OR dest_ip={hypothesis['indicator']}
        | stats count by src_ip, dest_ip
        """
```

### Threat Intelligence Integration

```python
class ThreatIntelligenceAI:
    """AI-powered threat intelligence"""
    
    def __init__(self):
        self.sources = [
            'alienvault',
            'virustotal',
            'threatfox',
            'abuseipdb'
        ]
        self.ai = ThreatIntelAI()
    
    def enrich_indicator(self, indicator: str) -> Dict:
        """Enrich indicator with threat intel"""
        
        # Query multiple sources
        results = {}
        for source in self.sources:
            results[source] = self.query_source(source, indicator)
        
        # AI analysis
        analysis = self.ai.correlate(results)
        
        return {
            'indicator': indicator,
            'sources': results,
            'analysis': analysis,
            'risk_score': analysis['risk_score']
        }
```

---

## 7.3 Incident Response Automation

### AI Incident Response

```python
class AIIncidentResponse:
    """AI-powered incident response"""
    
    def __init__(self):
        self.playbooks = self.load_playbooks()
        self.automation = ResponseAutomation()
    
    def handle_incident(self, incident: Dict) -> Dict:
        """Handle security incident"""
        
        # Classify incident
        classification = self.classify(incident)
        
        # Select playbook
        playbook = self.select_playbook(classification)
        
        # Execute response
        response = self.execute_playbook(playbook, incident)
        
        return response
    
    def classify(self, incident: Dict) -> Dict:
        """Classify incident using AI"""
        
        # Extract features
        features = self.extract_features(incident)
        
        # Predict classification
        incident_type = self.ml_model.classify(features)
        severity = self.ml_model.predict_severity(features)
        
        return {
            'type': incident_type,
            'severity': severity,
            'confidence': features['confidence']
        }
    
    def select_playbook(self, classification: Dict) -> str:
        """Select appropriate playbook"""
        
        type_to_playbook = {
            'malware': 'malware_response',
            'phishing': 'phishing_response',
            'intrusion': 'intrusion_response',
            'data_breach': 'breach_response'
        }
        
        return type_to_playbook.get(classification['type'], 'general_response')
```

### Playbook Automation

```python
class ResponsePlaybook:
    """Incident response playbook"""
    
    def __init__(self, name: str):
        self.name = name
        self.steps = []
    
    def add_step(self, step: Dict):
        """Add playbook step"""
        
        self.steps.append(step)
    
    def execute(self, incident: Dict) -> Dict:
        """Execute playbook"""
        
        results = []
        
        for step in self.steps:
            # Execute step
            result = self.execute_step(step, incident)
            results.append(result)
            
            # Check if we should continue
            if result['stop']:
                break
        
        return {
            'playbook': self.name,
            'steps_executed': len(results),
            'results': results,
            'success': all(r['success'] for r in results)
        }
    
    def execute_step(self, step: Dict, incident: Dict) -> Dict:
        """Execute single step"""
        
        action = step['action']
        
        if action == 'isolate':
            return self.isolate_host(incident['host'])
        elif action == 'block_ip':
            return self.block_ip(incident['indicator'])
        elif action == 'collect_evidence':
            return self.collect_evidence(incident)
        elif action == 'notify':
            return self.send_notification(incident)
        
        return {'success': True, 'stop': False}
```

---

## 7.4 AI Forensics Tools

### Digital Forensics with AI

```python
class AIForensics:
    """AI-powered forensics"""
    
    def __init__(self):
        self.evidence_collector = EvidenceCollector()
        self.ai_analyzer = ForensicsAI()
    
    def analyze_evidence(self, evidence_path: str) -> Dict:
        """Analyze forensic evidence"""
        
        # Collect evidence
        evidence = self.evidence_collector.collect(evidence_path)
        
        # AI analysis
        analysis = self.ai_analyzer.analyze(evidence)
        
        return {
            'evidence': evidence,
            'analysis': analysis,
            'timeline': analysis['timeline'],
            'findings': analysis['findings']
        }
    
    def build_timeline(self, evidence: list) -> List[Dict]:
        """Build incident timeline"""
        
        events = []
        
        for item in evidence:
            event = {
                'timestamp': item['timestamp'],
                'event': item['event'],
                'source': item['source'],
                'significance': self.ai_analyzer.assess_significance(item)
            }
            events.append(event)
        
        # Sort by timestamp
        return sorted(events, key=lambda x: x['timestamp'])
```

### Malware Forensics

```python
class MalwareForensics:
    """AI-powered malware forensics"""
    
    def __init__(self):
        self.ml_model = self.load_malware_model()
    
    def analyze_sample(self, sample_path: str) -> Dict:
        """Analyze malware sample"""
        
        # Static analysis
        static = self.static_analysis(sample_path)
        
        # Dynamic analysis  
        dynamic = self.dynamic_analysis(sample_path)
        
        # AI classification
        classification = self.ml_model.classify(static, dynamic)
        
        return {
            'static': static,
            'dynamic': dynamic,
            'classification': classification,
            'family': classification['family'],
            'capabilities': classification['capabilities']
        }
    
    def static_analysis(self, sample_path: str) -> Dict:
        """Static analysis"""
        
        return {
            'file_size': os.path.getsize(sample_path),
            'file_hash': self.calculate_hash(sample_path),
            'imports': self.extract_imports(sample_path),
            'strings': self.extract_strings(sample_path)
        }
    
    def dynamic_analysis(self, sample_path: str) -> Dict:
        """Dynamic analysis"""
        
        # Run in sandbox
        return {
            'network_calls': [],
            'file_operations': [],
            'registry_operations': [],
            'process_activity': []
        }
```

---

## 7.5 SOC Automation Playbooks

### Security Orchestration

```python
class SOCAutomation:
    """SOC automation framework"""
    
    def __init__(self):
        self.integrations = self.setup_integrations()
        self.playbooks = {}
    
    def setup_integrations(self):
        """Setup tool integrations"""
        
        return {
            'firewall': FirewallAPI(),
            'edr': EDRAPI(),
            'siem': SIEMAPI(),
            'ticketing': TicketingAPI(),
            'notification': NotificationAPI()
        }
    
    def run_playbook(self, playbook_name: str, incident: Dict):
        """Run automation playbook"""
        
        playbook = self.playbooks[playbook_name]
        
        for step in playbook.steps:
            self.execute_step(step, incident)
    
    def execute_step(self, step: Dict, incident: Dict):
        """Execute automation step"""
        
        tool = step['tool']
        action = step['action']
        
        if tool in self.integrations:
            api = self.integrations[tool]
            api.execute(action, incident)
```

### Complete Playbook Example

```python
# Example: Phishing Response Playbook
phishing_playbook = {
    'name': 'phishing_response',
    'steps': [
        {
            'tool': 'siem',
            'action': 'search',
            'params': {'query': 'phishing email indicators'}
        },
        {
            'tool': 'edr',
            'action': 'quarantine_email',
            'params': {'email_id': '${incident.email_id}'}
        },
        {
            'tool': 'firewall',
            'action': 'block_url',
            'params': {'url': '${incident.malicious_url}'}
        },
        {
            'tool': 'edr',
            'action': 'scan_endpoint',
            'params': {'endpoint': '${incident.target_endpoint}'}
        },
        {
            'tool': 'ticketing',
            'action': 'create_ticket',
            'params': {'incident': 'incident'}
        },
        {
            'tool': 'notification',
            'action': 'notify',
            'params': {'channels': ['email', 'slack']}
        }
    ]
}
```

---

## 7.6 Hands-On Lab

### Lab 7.1: Build Simple Alert System

```python
class SimpleAlertSystem:
    """Build simple security alert system"""
    
    def __init__(self):
        self.alerts = []
        self.thresholds = {
            'failed_logins': 5,
            'bandwidth_mb': 1000,
            'cpu_percent': 90
        }
    
    def check_metrics(self, metrics: dict):
        """Check metrics against thresholds"""
        
        for metric, value in metrics.items():
            if metric in self.thresholds:
                if value > self.thresholds[metric]:
                    self.create_alert(metric, value)
    
    def create_alert(self, metric: str, value: float):
        """Create security alert"""
        
        alert = {
            'metric': metric,
            'value': value,
            'threshold': self.thresholds[metric],
            'severity': self.get_severity(value, self.thresholds[metric]),
            'timestamp': datetime.now()
        }
        
        self.alerts.append(alert)
        print(f"ALERT: {metric} exceeded threshold!")
    
    def get_severity(self, value: float, threshold: float) -> str:
        """Calculate severity"""
        
        ratio = value / threshold
        
        if ratio > 2:
            return 'critical'
        elif ratio > 1.5:
            return 'high'
        else:
            return 'medium'
```

---

## Module 7 Summary

### Key Takeaways

1. **AI SIEM** provides intelligent log analysis
2. **Threat hunting** is automated with AI
3. **Incident response** becomes faster with playbooks
4. **Forensics** enhanced by AI analysis
5. **SOC automation** streamlines operations

### SOC Tools

| Tool | Purpose | AI Enhancement |
|------|---------|---------------|
| Splunk | SIEM | ML analytics |
| Elastic | SIEM | ML detection |
| IBM QRadar | SIEM | Watson AI |
| Microsoft Sentinel | SIEM | Azure ML |

### Playbook Types

| Type | Trigger | Response |
|------|---------|----------|
| Phishing | Email detected | Quarantine, block |
| Malware | File detected | Isolate, scan |
| Intrusion | Alert triggered | Contain, investigate |
| Data breach | DLP alert | Preserve evidence |

### Next Steps

Proceed to **Module 8: AI Security Tools** to learn about building and using AI security tools.

---

## Quick Reference

```python
# Quick SOC automation
def handle_incident(incident):
    classify = ai_classify(incident)
    playbook = get_playbook(classify)
    execute_playbook(playbook, incident)
    notify_stakeholders(incident)
    create_ticket(incident)
```
