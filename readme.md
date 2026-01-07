## What is Continuous Testing?
Continuous Testing means **automatically running API tests whenever code changes** using a CI tool.

## 🛠 Tools Used
- Postman – API testing
- Newman – Run Postman tests from command line
- Git – Version control
- Jenkins – CI/CD automation
  
## ▶ How to Run Tests
1. Push Postman tests to GitHub  
2. Jenkins pulls the code  
3. Newman runs API tests  
4. HTML report is generated  

## 📊 Test Report
After Jenkins build:
- Go to Jenkins Job
- Open **Postman API Test Report**
