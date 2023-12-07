agile devops

### devops culture as google sees it.

1. Reduce organizational silos
2. Accept failure as normal
3. Implement gradual change
4. Leverage tooling and automation
5. Measure everything



# Pipeline


1. plan -> trello, jira, github environment 
2. git  commit and automation ( github actions) -> github actions configured with yaml files.
3. gitkraken -> git timeline overview of history
4. static code analysis -> test the systax , endless loops, (sonarcloud) before building 
5. build -> maven(java), npm(javascript),...
		-> from lines of code to an string of bits.
5. unit tests
	1. -> testing all functions
6. integration tests.
	1. does the application what it need to do with real data, real database (staging)
7. load test, can the application handle stress (locust)
8. in-browser tests (selenium)
9. containerize and store
10. Deploy (heroku,kubernetes)
11. monitor (prometheus, contrast security monitoring)