<div align="center">

# 🏥 OpenEMR Automation

### BDD UI test framework for the OpenEMR electronic medical record system

[![Typing SVG](https://readme-typing-svg.demolab.com/?font=Fira+Code&size=18&pause=1500&color=FFC107&center=true&vCenter=true&width=900&repeat=true&lines=Java+%C2%B7+Selenium+4+%C2%B7+Cucumber+7+%C2%B7+TestNG+%C2%B7+Maven;Healthcare+QA%3A+login%2C+patient+registration%2C+form+validation%2C+logout;5+%2F+5+scenarios+passing+on+demo.openemr.io)](https://git.io/typing-svg)

<!-- ============ STATUS BAR ============ -->
![Status](https://img.shields.io/badge/Status-Stable-0d9488?style=for-the-badge&logo=checkmarx&logoColor=white)
![Pass Rate](https://img.shields.io/badge/Pass%20Rate-100%25%20(5%2F5)-22c55e?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-Healthcare%20%C2%B7%20EMR-155e75?style=for-the-badge)
![Target](https://img.shields.io/badge/Target-demo.openemr.io-1e3a8a?style=for-the-badge&logo=googlechrome&logoColor=white)

![Java](https://img.shields.io/badge/Java-11%2B-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium-4.18.1-43B02A?style=for-the-badge&logo=selenium&logoColor=white)
![Cucumber](https://img.shields.io/badge/Cucumber-7.15.0-23D96C?style=for-the-badge&logo=cucumber&logoColor=white)
![TestNG](https://img.shields.io/badge/TestNG-7.9.0-FF7F00?style=for-the-badge)
![Maven](https://img.shields.io/badge/Maven-Build-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white)

![Last Commit](https://img.shields.io/github/last-commit/rbchy/OpenEMR_Automation?style=flat-square&color=0d9488&label=Last%20commit)
![Repo Size](https://img.shields.io/github/repo-size/rbchy/OpenEMR_Automation?style=flat-square&color=155e75&label=Repo%20size)
![Top Language](https://img.shields.io/github/languages/top/rbchy/OpenEMR_Automation?style=flat-square&color=f59e0b)

</div>

---

## 📌 At a Glance

<table>
<tr>
<td width="50%" valign="top">

**🙋 What this is**

A UI automation framework that tests **[OpenEMR](https://www.open-emr.org/)**, the open-source electronic medical record and practice management system, through its public demo. Scenarios are written in plain-English **Gherkin**, backed by **Page Object** classes and run by **TestNG** through Maven, with a screenshot attached to the report whenever a scenario fails.

> *Healthcare software has no room for a silent failure: if a patient cannot be registered, the test must say so.*

</td>
<td width="50%" valign="top">

**📍 Quick facts**

| | |
|---|---|
| 🎯 **Application** | [demo.openemr.io](https://demo.openemr.io/openemr/interface/login/login.php) |
| 🧪 **Scenarios** | 5 (3 `@smoke` · 2 `@regression`) |
| ✅ **Latest run** | 5 / 5 passed · 2 m 22 s |
| 💻 **Run on** | macOS · OpenJDK 21 · Chrome |
| 📄 **Report** | [Cucumber HTML report (PDF)](OpenEMR%20Cucumber%20Test%20Report.pdf) |

</td>
</tr>
</table>

---

## ✅ Latest Results

| Feature | Scenario | Tag | Result |
|---|---|---|---|
| 🔐 OpenEMR Login | Successful login (admin user, English language) | `@smoke` | ![passed](https://img.shields.io/badge/-passed-22c55e?style=flat-square) |
| 🔐 OpenEMR Login (`openemr.feature`) | Successful login | `@smoke` | ![passed](https://img.shields.io/badge/-passed-22c55e?style=flat-square) |
| 👤 Patient Management | Add new patient successfully | `@smoke` | ![passed](https://img.shields.io/badge/-passed-22c55e?style=flat-square) |
| 👤 Patient Management | Add patient with missing mandatory fields → *"First Name is required"* | `@regression` | ![passed](https://img.shields.io/badge/-passed-22c55e?style=flat-square) |
| ⚙️ OpenEMR Admin Actions | Logout successfully | `@regression` | ![passed](https://img.shields.io/badge/-passed-22c55e?style=flat-square) |

<sub>Source: the Cucumber report in this repository (cucumber-jvm 7.15.0, OpenJDK 21.0.7, macOS). The demo site is shared and reset regularly, so results depend on its availability.</sub>

---

## 🛠️ Tech Stack

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Language | Java | 11 (runs on 11–21) | Test code |
| Browser automation | Selenium WebDriver | 4.18.1 | Drives Chrome |
| Driver management | WebDriverManager | 5.8.0 | Downloads the matching ChromeDriver automatically |
| BDD | Cucumber JVM (Gherkin) | 7.15.0 | Readable Given / When / Then scenarios |
| Test runner | TestNG + `cucumber-testng` | 7.9.0 | Runs features, tag-based suites |
| Build | Maven (Surefire 3.2.5) | — | Dependencies and test execution |
| Reporting | Cucumber HTML / JSON / JUnit XML | — | `target/` reports, failure screenshots |
| IDE | Eclipse / IntelliJ IDEA | — | Development |

---

## 🏗️ Framework Architecture

```mermaid
flowchart LR
  F["Feature files<br/>(Gherkin)"] --> S["Step definitions<br/>stepdefinitions/"]
  S --> P["Page Objects<br/>pages/"]
  P --> W["Selenium WebDriver<br/>+ WebDriverManager"]
  W --> C["Chrome"]
  C --> O["OpenEMR<br/>demo.openemr.io"]
  H["Hooks<br/>@Before / @After"] -.->|"start browser ·<br/>screenshot on failure · quit"| W
  R["Runners<br/>TestRunner · Smoke · Regression · Sanity"] --> F
```

**Design patterns applied**

- **Page Object Model** — each screen (Login, Patient, Admin, Insurance) keeps its own locators and actions
- **BDD with Cucumber** — scenarios read as plain English for testers, developers and clinical stakeholders
- **Hooks** — a fresh Chrome per scenario; a PNG screenshot is attached to the report on failure
- **Tag-based runners** — one runner per suite (`@smoke`, `@regression`, `@sanity`) plus a combined runner
- **Explicit waits** — `WaitUtils` and `WebDriverWait` for menus and iframe-hosted forms

---

## 📁 Project Structure

```
OpenEMR_Automation/
├── src/test/java/
│   ├── base/
│   │   └── BaseClass.java            ← shared driver setup
│   ├── pages/                        ← Page Object Model
│   │   ├── LoginPage.java            ← username, password, language, login
│   │   ├── PatientPage.java          ← Patient › New/Search, demographics form
│   │   ├── AdminPage.java            ← Admin menu, logout
│   │   └── InsurancePage.java        ← insurance entry inside the patient frame
│   ├── stepdefinitions/
│   │   ├── Hooks.java                ← @Before / @After, failure screenshots
│   │   ├── LoginSteps.java
│   │   ├── PatientSteps.java
│   │   ├── AdminSteps.java
│   │   └── OpenEMRSteps.java
│   ├── runners/
│   │   ├── TestRunner.java           ← @smoke or @regression (default)
│   │   ├── SmokeRunner.java
│   │   ├── RegressionRunner.java
│   │   └── SanityRunner.java
│   └── utils/
│       ├── DriverFactory.java
│       ├── DriverManager.java
│       └── WaitUtils.java
├── src/test/resources/features/
│   ├── login.feature
│   ├── openemr.feature
│   ├── patient.feature
│   └── admin.feature
├── OpenEMR Cucumber Test Report.pdf  ← latest run, exported from the HTML report
├── pom.xml
└── testng.xml
```

---

## 🎯 Test Coverage

<details open>
<summary><strong>🔐 Authentication</strong></summary>

<br>

- Open the OpenEMR login page, enter credentials, pick the interface language
- Confirm the dashboard loads after a successful login
- Log out from the **Admin** menu

</details>

<details>
<summary><strong>👤 Patient Management</strong></summary>

<br>

- Navigate **Patient › New/Search** and fill the demographics form (first name, last name, date of birth, sex)
- Save the record and confirm the patient is created
- Negative test: leave **First Name** empty and verify the *"First Name is required"* validation message

</details>

<details>
<summary><strong>🧾 Insurance (page object ready)</strong></summary>

<br>

- `InsurancePage` adds a provider and policy number inside the patient frame (`pat`); a feature file for it is on the roadmap

</details>

---

## ⚙️ Getting Started

**Prerequisites:** JDK 11 or newer · Maven 3.8+ · Google Chrome · Git
No manual ChromeDriver download is needed — WebDriverManager fetches the right version.

```bash
git clone https://github.com/rbchy/OpenEMR_Automation.git
cd OpenEMR_Automation
mvn clean install -DskipTests
```

---

## ▶️ Running the Tests

```bash
# Default suite: @smoke or @regression (TestRunner)
mvn clean test

# One suite by runner
mvn clean test -Dtest=SmokeRunner
mvn clean test -Dtest=RegressionRunner

# Any tag expression
mvn clean test -Dcucumber.filter.tags="@smoke"
```

**From the IDE:** right-click `runners/TestRunner.java` (or `testng.xml`) → **Run As › TestNG Test**.

**Reports** are written to `target/` after every run:

| File | Format |
|---|---|
| `target/cucumber-report.html` | Cucumber HTML report (with failure screenshots) |
| `target/cucumber.json` | JSON, for Allure / Jenkins plugins |
| `target/cucumber.xml` | JUnit XML, for CI test summaries |
| `target/smoke-report.html`, `regression-report.html`, `sanity-report.html` | Per-suite HTML reports |

---

## 🏷️ Tags

| Tag | Meaning | Scenarios |
|---|---|---|
| `@smoke` | Critical path — build verification | 3 |
| `@regression` | Negative and end-to-end flows | 2 |
| `@sanity` | Reserved for quick post-deploy checks | 0 |

---

## ⚠️ Healthcare Data Notice

> This framework runs only against the **public OpenEMR demo**, using the demo's published credentials. All test data (for example *John Doe, 1980-01-01*) is synthetic.

- Never use real patient information in a test scenario
- Treat even test environments with HIPAA-minded care: no real PHI in data, logs or screenshots
- The demo is shared and reset regularly; do not rely on records persisting between runs

---

## 📈 Roadmap

- [ ] Allure reports with step screenshots
- [ ] GitHub Actions workflow running headless Chrome on every push
- [ ] Parallel execution (`@DataProvider(parallel = true)`) with a thread-safe driver
- [ ] Cross-browser: Firefox and Edge
- [ ] Insurance, appointment scheduling and encounter scenarios
- [ ] Data-driven patients from JSON / Excel
- [ ] REST Assured checks against the OpenEMR REST / FHIR API
- [ ] Credentials moved to a config file / environment variables

---

## 🔗 Related Projects

| Project | Stack |
|---|---|
| ⭐ [RbcTcsWorld E-Commerce Suite](https://github.com/rbchy/RbcTcsWorld_ECommerceSuite) | Spring Boot · REST Assured · Selenium · Playwright · Appium · CI quality gates |
| 🧪 [ClinTrial-Connect](https://github.com/rbchy/RbcTcsWorld_ClinTrial-Connect) | Spring Boot · Java (clinical trials) |
| 🏭 [PPES Pharma Packaging](https://github.com/rbchy/PPES-Pharmaceutical-Packaging-Management) | Java 17 · MySQL 8 |
| ☁️ [Sauce Labs Cloud Automation](https://github.com/rbchy/QaBrainsSauceLabAPI_Automation) | Selenium · Cucumber · Sauce Labs |

<sub>All projects: [github.com/rbchy](https://github.com/rbchy)</sub>

---

## 👤 Author

<div align="center">

**Ranajit Baran Chowdhury (RB Chowdhury)**
QA Automation Engineer / SDET · West Norriton, Pennsylvania, USA

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rbchy/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/rbchy)
[![Website](https://img.shields.io/badge/Website-rbchy.github.io%2Frbchy-0d9488?style=for-the-badge&logo=githubpages&logoColor=white)](https://rbchy.github.io/rbchy/)
[![Portfolio](https://img.shields.io/badge/Portfolio-Website-blueviolet?style=for-the-badge&logo=wix&logoColor=white)](https://rbc6543.wixsite.com/rbc-portfolio)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:chyranajit@gmail.com)

<sub>Provided for educational and professional QA automation purposes. OpenEMR is © its contributors and licensed under GPL; this repository only tests its public demo.</sub>

⭐ *If this framework helps you, a star on the repo is appreciated.*

</div>
