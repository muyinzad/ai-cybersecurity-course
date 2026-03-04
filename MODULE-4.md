# Module 4: AI-Powered Reconnaissance

## Overview

This module covers how AI enhances reconnaissance activities - from automated OSINT gathering to intelligent vulnerability scanning. Learn to build AI-powered recon tools.

---

## 4.1 Automated OSINT with AI

### AI-Enhanced Information Gathering

```python
import requests
import json
from typing import List, Dict

class AIOsintCollector:
    """AI-powered OSINT collection"""
    
    def __init__(self):
        self.sources = {
            'shodan': ShodanAPI(),
            'censys': CensysAPI(),
            'virustotal': VirusTotalAPI(),
            'hunter': HunterAPI()
        }
        self.ai_analyzer = AIAnalyzer()
    
    def collect_all(self, target: str) -> Dict:
        """Collect OSINT from all sources"""
        
        results = {
            'domain': {},
            'ip': {},
            'email': {},
            'social': {}
        }
        
        # Domain enumeration
        results['domain'] = self.enumerate_domains(target)
        
        # IP discovery
        results['ip'] = self.discover_ips(target)
        
        # Email harvesting
        results['email'] = self.harvest_emails(target)
        
        # Social media
        results['social'] = self.find_social_media(target)
        
        # AI Analysis
        results['ai_analysis'] = self.ai_analyzer.analyze(results)
        
        return results
    
    def enumerate_domains(self, target: str) -> Dict:
        """Enumerate subdomains using AI"""
        
        subdomains = []
        
        # Common subdomain wordlist
        common = ['www', 'mail', 'ftp', 'admin', 'api', 'dev', 'test']
        
        for sub in common:
            domain = f"{sub}.{target}"
            if self.check_exists(domain):
                subdomains.append(domain)
        
        # Use AI to discover more
        ai_subdomains = self.ai_analyzer.predict_subdomains(target)
        subdomains.extend(ai_subdomains)
        
        return {'subdomains': subdomains}
    
    def discover_ips(self, target: str) -> Dict:
        """Discover IP addresses"""
        
        # DNS resolution
        try:
            ip = self.resolve_dns(target)
        except:
            ip = None
        
        # Reverse DNS
        reverse_dns = self.reverse_dns_lookup(ip)
        
        return {
            'primary_ip': ip,
            'reverse_dns': reverse_dns
        }
    
    def harvest_emails(self, target: str) -> List[str]:
        """Harvest email addresses"""
        
        emails = []
        
        # Hunter.io
        hunter_results = self.sources['hunter'].search(target)
        emails.extend(hunter_results)
        
        # Use AI to generate likely emails
        ai_emails = self.ai_analyzer.generate_emails(target)
        emails.extend(ai_emails)
        
        return list(set(emails))
```

### AI Email Pattern Analysis

```python
class AIEmailAnalyzer:
    """AI-powered email analysis"""
    
    def __init__(self):
        self.pattern_model = self.load_pattern_model()
    
    def analyze_patterns(self, known_emails: List[str]) -> Dict:
        """Analyze email patterns"""
        
        # Extract pattern
        pattern = self.extract_pattern(known_emails)
        
        # Predict variations
        variations = self.predict_variations(pattern)
        
        return {
            'pattern': pattern,
            'variations': variations,
            'confidence': 0.85
        }
    
    def generate_likely_emails(self, first_name: str, last_name: str, domain: str) -> List[str]:
        """Generate likely email addresses"""
        
        patterns = [
            f"{first_name}.{last_name}@{domain}",
            f"{first_name}{last_name}@{domain}",
            f"{first_name[0]}{last_name}@{domain}",
            f"{first_name}{last_name[0]}@{domain}",
            f"{first_name}_{last_name}@{domain}",
        ]
        
        return patterns
```

---

## 4.2 Smart Subdomain Enumeration

### AI-Enhanced Enumeration

```python
import dns.resolver
import asyncio

class AISubdomainEnumerator:
    """AI-powered subdomain enumeration"""
    
    def __init__(self):
        self.wordlist = self.load_wordlist()
        self.ai_predictor = SubdomainPredictor()
    
    def enumerate(self, domain: str) -> List[str]:
        """Enumerate subdomains with AI assistance"""
        
        results = []
        
        # Traditional enumeration
        results.extend(self.brute_force(domain))
        
        # AI-enhanced discovery
        results.extend(self.ai_predictor.discover(domain))
        
        # Certificate transparency
        results.extend(self.cert_search(domain))
        
        return list(set(results))
    
    def brute_force(self, domain: str) -> List[str]:
        """Traditional brute force"""
        
        found = []
        
        for word in self.wordlist:
            subdomain = f"{word}.{domain}"
            
            try:
                answers = dns.resolver.resolve(subdomain, 'A')
                if answers:
                    found.append(subdomain)
            except:
                pass
        
        return found
    
    def ai_predictor_discover(self, domain: str) -> List[str]:
        """Use AI to predict subdomains"""
        
        # Train on known subdomains
        known = self.get_known_subdomains(domain)
        
        # Predict new ones
        predictions = self.ai_predictor.predict(known, domain)
        
        return predictions
```

### DNS Analysis with AI

```python
class AIDNSAnalyzer:
    """AI-powered DNS analysis"""
    
    def __init__(self):
        self.ml_model = self.load_model()
    
    def analyze_dns_records(self, domain: str) -> Dict:
        """Analyze DNS records for anomalies"""
        
        records = {
            'A': self.get_records(domain, 'A'),
            'AAAA': self.get_records(domain, 'AAAA'),
            'MX': self.get_records(domain, 'MX'),
            'TXT': self.get_records(domain, 'TXT'),
            'NS': self.get_records(domain, 'NS'),
            'CNAME': self.get_records(domain, 'CNAME')
        }
        
        # AI analysis
        anomalies = self.ml_model.detect_anomalies(records)
        
        return {
            'records': records,
            'anomalies': anomalies,
            'risk_score': self.calculate_risk(anomalies)
        }
```

---

## 4.3 AI-Driven Vulnerability Scanning

### Smart Vulnerability Scanner

```python
class AIVulnerabilityScanner:
    """AI-powered vulnerability scanner"""
    
    def __init__(self, target: str):
        self.target = target
        self.findings = []
        self.ai_analyzer = VulnerabilityAI()
    
    def scan(self) -> Dict:
        """Run comprehensive scan"""
        
        phases = [
            self.scan_ports,
            self.scan_services,
            self.scan_web,
            self.scan_config
        ]
        
        for phase in phases:
            results = phase()
            self.findings.extend(results)
        
        # AI prioritization
        prioritized = self.ai_analyzer.prioritize(self.findings)
        
        return {
            'findings': prioritized,
            'risk_score': self.calculate_total_risk(prioritized)
        }
    
    def scan_ports(self) -> List[Dict]:
        """Scan ports with AI"""
        
        common_ports = [21, 22, 23, 25, 80, 443, 3306, 3389, 5432, 8080]
        
        findings = []
        
        for port in common_ports:
            if self.is_open(port):
                service = self.identify_service(port)
                
                # AI vulnerability check
                vulns = self.ai_analyzer.check_service_vulns(service)
                
                findings.append({
                    'port': port,
                    'service': service,
                    'vulnerabilities': vulns
                })
        
        return findings
    
    def scan_web(self) -> List[Dict]:
        """Scan web applications"""
        
        findings = []
        
        # Crawl website
        pages = self.crawl(self.target)
        
        for page in pages:
            # Check for vulnerabilities
            vulns = self.check_web_vulns(page)
            findings.extend(vulns)
        
        return findings
```

### AI Vulnerability Prediction

```python
class VulnerabilityPredictor:
    """Predict vulnerabilities using ML"""
    
    def __init__(self):
        self.model = self.load_pretrained_model()
    
    def predict(self, service_info: Dict) -> List[Dict]:
        """Predict likely vulnerabilities"""
        
        features = self.extract_features(service_info)
        
        predictions = self.model.predict(features)
        
        vulnerabilities = []
        
        for pred in predictions:
            if pred['probability'] > 0.7:
                vulnerabilities.append({
                    'type': pred['vulnerability_type'],
                    'probability': pred['probability'],
                    'severity': pred['severity'],
                    'exploitability': pred['exploitability']
                })
        
        return vulnerabilities
```

---

## 4.4 Passive Discovery Automation

### Passive Reconnaissance

```python
class PassiveRecon:
    """Passive reconnaissance automation"""
    
    def __init__(self):
        self.sources = [
            ShodanSearch(),
            CensysSearch(),
            PassiveDNS(),
            CertificateSearch()
        ]
    
    def discover(self, target: str) -> Dict:
        """Discover information passively"""
        
        results = {
            'passive_dns': [],
            'certificates': [],
            'historical': [],
            'leaked_data': []
        }
        
        # Query all passive sources
        for source in self.sources:
            data = source.query(target)
            results[type(source).__name__] = data
        
        return results
```

### Search Engine Automation

```python
class SearchEngineRecon:
    """Automated search engine reconnaissance"""
    
    def __init__(self):
        self.engines = ['google', 'bing', 'duckduckgo']
    
    def search(self, query: str) -> List[Dict]:
        """Search multiple engines"""
        
        results = []
        
        for engine in self.engines:
            engine_results = self.search_engine(engine, query)
            results.extend(engine_results)
        
        return results
    
    def dorking(self, target: str) -> List[Dict]:
        """Perform Google dorking"""
        
        dorks = [
            f"site:{target} ext:sql OR ext:db OR ext:mdb",
            f"site:{target} inurl:admin",
            f"site:{target} inurl:login",
            f'site:{target} "password"',
            f"site:{target} filetype:pdf",
        ]
        
        results = []
        
        for dork in dorks:
            results.extend(self.search(dork))
        
        return results
```

---

## 4.5 AI for Social Engineering

### Social Engineering Automation

```python
class AISocialEngineering:
    """AI-powered social engineering"""
    
    def __init__(self):
        self.target_profiler = TargetProfiler()
        self.email_generator = EmailGenerator()
    
    def profile_target(self, target_email: str) -> Dict:
        """Profile a target"""
        
        # Gather information
        info = {
            'email': target_email,
            'domain': target_email.split('@')[1],
            'name': self.extract_name(target_email),
            'company': self.find_company(target_email),
            'social_media': self.find_social(target_email)
        }
        
        # AI analysis
        profile = self.target_profiler.analyze(info)
        
        return profile
    
    def generate_personalized_attack(self, profile: Dict) -> str:
        """Generate personalized attack content"""
        
        # Generate phishing email
        email = self.email_generator.generate(
            target_info=profile,
            scenario='urgent_request'
        )
        
        return email
```

---

## 4.6 Recon Automation Framework

### Complete Framework

```python
class ReconFramework:
    """Complete reconnaissance framework"""
    
    def __init__(self, target: str):
        self.target = target
        self.modules = {
            'osint': AIOsintCollector(),
            'subdomains': AISubdomainEnumerator(),
            'vulns': AIVulnerabilityScanner(),
            'passive': PassiveRecon()
        }
        self.results = {}
    
    def run_full_recon(self) -> Dict:
        """Run complete reconnaissance"""
        
        print(f"Starting reconnaissance on {self.target}")
        
        # Phase 1: Passive
        print("[1/4] Passive reconnaissance...")
        self.results['passive'] = self.modules['passive'].discover(self.target)
        
        # Phase 2: Subdomains
        print("[2/4] Subdomain enumeration...")
        self.results['subdomains'] = self.modules['subdomains'].enumerate(self.target)
        
        # Phase 3: Active
        print("[3/4] Active scanning...")
        self.results['vulnerabilities'] = self.modules['vulns'].scan()
        
        # Phase 4: Analysis
        print("[4/4] AI analysis...")
        self.results['analysis'] = self.ai_analyze()
        
        return self.results
    
    def ai_analyze(self) -> Dict:
        """AI analysis of results"""
        
        return {
            'attack_surface': self.calculate_attack_surface(),
            'high_value_targets': self.identify_high_value(),
            'recommended_attacks': self.recommend_attacks()
        }
```

---

## 4.7 Hands-On Lab

### Lab 4.1: Build a Simple Scanner

```python
class SimpleScanner:
    """Build a simple AI scanner"""
    
    def __init__(self):
        self.findings = []
    
    def scan(self, target: str) -> List[Dict]:
        """Simple port scanner"""
        
        common_ports = [80, 443, 22, 21, 25, 3306, 8080]
        
        for port in common_ports:
            if self.is_open(target, port):
                self.findings.append({
                    'port': port,
                    'service': self.get_service(port),
                    'severity': self.get_severity(port)
                })
        
        return self.findings
    
    def is_open(self, target: str, port: int) -> bool:
        """Check if port is open"""
        # Simplified
        return False
    
    def get_service(self, port: int) -> str:
        """Get service name"""
        services = {80: 'http', 443: 'https', 22: 'ssh'}
        return services.get(port, 'unknown')
    
    def get_severity(self, port: int) -> str:
        """Get severity level"""
        critical = [21, 23, 3306]
        high = [22, 3389]
        medium = [80, 443, 8080]
        
        if port in critical:
            return 'critical'
        elif port in high:
            return 'high'
        return 'medium'
```

---

## Module 4 Summary

### Key Takeaways

1. **AI enhances** OSINT collection and analysis
2. **Smart enumeration** discovers more subdomains
3. **ML-powered scanners** find vulnerabilities faster
4. **Passive recon** reduces detection risk
5. **Frameworks** automate the entire process

### Tools Covered

| Tool | Purpose | AI Enhancement |
|------|---------|---------------|
| Shodan | Internet scanning | ML filtering |
| Censys | Network discovery | Anomaly detection |
| VirusTotal | Threat intelligence | Pattern analysis |
| Custom tools | Custom recon | Custom ML |

### Next Steps

Proceed to **Module 5: AI Exploitation Tools** to learn about AI-powered attack tools.

---

## Quick Reference

| Technique | Use Case | Risk |
|-----------|----------|------|
| Subdomain enum | Discovery | Medium |
| Port scanning | Service identification | High |
| Web crawling | Application mapping | Medium |
| Passive recon | Stealthy gathering | Low |
| Social engineering | Target-specific | High |
