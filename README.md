# Thingsboard: Penetration-Test and Vulnerabilities finding

## Table des Matières
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Static vs. Dynamic Code Analysis](#static-and-dynamic-code-analysis) 


## Installation

[Trivy (git)](https://github.com/aquasecurity/trivy)
<br>
[OWASP ZAP (git)](https://github.com/zaproxy/zaproxy)
<br>
[SpotBugs (git)](https://github.com/spotbugs/spotbugs)

## Utilisation

Trivy: Static code analysis<br>
OWASP ZAP: Dynamic code analysis<br>
SpotBugs: Static code analysis<br>

## Static vs. Dynamic Code Analysis

**Static Code Analysis:**

Static code analysis is a method of analyzing software code without executing it. It involves examining the code's structure, syntax, and other static attributes to identify potential issues such as coding errors, security vulnerabilities, and compliance violations. Static analysis tools analyze the code as it is written or during the build process, typically without the need to run the software. This method is often used to detect issues early in the development lifecycle, as it can uncover potential problems before the code is executed.

**Key Points**:
- Analyzes code without executing it.
- Examines the structure and syntax of the code.
- Identifies potential issues such as coding errors and security vulnerabilities.
- Can be automated and integrated into the development process.
- Provides early detection of issues, reducing the likelihood of bugs and vulnerabilities in the final product.
- Examples include linting tools, code review tools, and static analysis security testing (SAST) tools.

**Dynamic Code Analysis:**

Dynamic code analysis, also known as dynamic testing, involves analyzing software code while it is running. It focuses on observing the behavior of the code in real-time, typically through testing scenarios such as unit tests, integration tests, and system tests. Dynamic analysis tools monitor the code's execution, input/output behavior, memory usage, and other runtime characteristics to identify issues such as runtime errors, performance bottlenecks, and security vulnerabilities that may only manifest during execution.

**Key Points**:
- Analyzes code while it is running.
- Observes the behavior of the code in real-time.
- Identifies runtime errors, performance issues, and security vulnerabilities.
- Requires executing the code through testing scenarios.
- Provides insights into the code's runtime behavior and performance characteristics.
- Examples include unit testing frameworks, code coverage tools, and dynamic analysis security testing (DAST) tools.

**Difference:**

The main difference between static and dynamic code analysis lies in when and how they analyze the code. Static analysis occurs without executing the code, focusing on its structure and syntax, while dynamic analysis happens during code execution, observing its behavior and runtime characteristics. Both approaches are valuable for identifying different types of issues and ensuring the overall quality and security of software applications.


