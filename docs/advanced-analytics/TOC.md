# 개요
## [SQL Server Machine Learning Services란?](what-is-sql-server-machine-learning.md)
## [새로운 기능](what-s-new-in-sql-server-machine-learning-services.md)
## [아키텍처 개요](architecture-overview-machine-learning.md)
## [버전별 기능](r/differences-in-r-features-between-editions-of-sql-server.md)

# [Machine Learning Services - R](r/sql-server-r-services.md)

## [시작](r/getting-started-with-sql-server-r-services.md)
### [SQL Server Machine Learning Services 설정(데이터베이스 내)](r/set-up-sql-server-r-services-in-database.md)
### [Machine Learning Services의 무인 설치](r/unattended-installs-of-sql-server-r-services.md)

## [아키텍처](r/architecture-overview-sql-server-r.md)
### [R 상호 운용성](r/r-interoperability-in-sql-server.md)
### [R 통합을 지원하는 구성 요소](r/new-components-in-sql-server-to-support-r.md)
### [R에 대한 보안](r/security-overview-sql-server-r.md)

## [모니터링](r/monitoring-r-services.md)

## [SQL Server용 R 자습서](tutorials/sql-server-r-tutorials.md)

### [R: Transact-SQL에서 R 코드 사용](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
#### [입/출력 작업](tutorials/rtsql-working-with-inputs-and-outputs.md)
#### [R 및 SQL 데이터 형식 및 데이터 개체](tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)
#### [R 함수를 SQL Server 데이터와 함께 사용](tutorials/rtsql-using-r-functions-with-sql-server-data.md)
#### [예측 모델 만들기](tutorials/rtsql-create-a-predictive-model-r.md)
#### [모델에서 예측 및 그리기](tutorials/rtsql-predict-and-plot-from-model.md)

### [R: 데이터 과학 종단 간 연습](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
#### [데이터 과학 연습을 위한 필수 조건](tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)
#### [데이터 준비](tutorials/walkthrough-prepare-the-data.md)
#### [SQL을 사용하여 데이터 탐색](tutorials/walkthrough-view-and-explore-the-data.md)
#### [R을 사용하여 데이터 요약](tutorials/walkthrough-view-and-summarize-data-using-r.md)
#### [R을 사용하여 그래프 및 플롯 만들기](tutorials/walkthrough-create-graphs-and-plots-using-r.md)
#### [SQL 및 R을 사용하여 데이터 기능 만들기](tutorials/walkthrough-create-data-features.md)
#### [모델 작성 및 저장](tutorials/walkthrough-build-and-save-the-model.md)
#### [모델 배포 및 사용](tutorials/walkthrough-deploy-and-use-the-model.md)

### [R: RevoScaleR로 데이터 과학 심층 분석](tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
#### [SQL Server 데이터 작업](tutorials/deepdive-work-with-sql-server-data-using-r.md)
#### [RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
#### [SQL Server 데이터 쿼리 및 수정](tutorials/deepdive-query-and-modify-the-sql-server-data.md)
#### [계산 컨텍스트 정의 및 사용](tutorials/deepdive-define-and-use-compute-contexts.md)
#### [R 스크립트 만들기 및 실행](tutorials/deepdive-create-and-run-r-scripts.md)
#### [R을 사용하여 SQL Server 데이터 시각화](tutorials/deepdive-visualize-sql-server-data-using-r.md)
#### [모델 만들기](tutorials/deepdive-create-models.md)
#### [새 데이터 점수 매기기](tutorials/deepdive-score-new-data.md)
#### [R을 사용하여 데이터 변환](tutorials/deepdive-transform-data-using-r.md)
#### [rxImport를 사용하여 메모리에 데이터 로드](tutorials/deepdive-load-data-into-memory-using-rximport.md)
#### [rxDataStep을 사용하여 새 SQL Server 테이블 만들기](tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
#### [rxDataStep을 사용하여 청크 분석 수행](tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
#### [로컬 계산 컨텍스트에서 데이터 분석](tutorials/deepdive-analyze-data-in-local-compute-context.md)
#### [SQL Server와 XDF 파일 간에 데이터 이동](tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
#### [간단한 시뮬레이션 만들기](tutorials/deepdive-create-a-simple-simulation.md)

### [R: SQL 개발자를 위한 데이터베이스 내 분석](tutorials/sqldev-in-database-r-for-sql-developers.md)
#### [1단계: 샘플 데이터 다운로드](tutorials/sqldev-download-the-sample-data.md)
#### [2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](r/sqldev-import-data-to-sql-server-using-powershell.md)
#### [3단계: 데이터 탐색 및 시각화](tutorials/sqldev-explore-and-visualize-the-data.md)
#### [4단계: T-SQL을 사용하여 데이터 기능 만들기](tutorials/sqldev-create-data-features-using-t-sql.md)
#### [5단계: T-SQL을 사용하여 모델 학습 및 저장](r/sqldev-train-and-save-a-model-using-t-sql.md)
#### [6단계: 모델 운영화](tutorials/sqldev-operationalize-the-model.md)


# [Machine Learning Services - Python](python/sql-server-python-services.md)

## [시작](python/setup-python-machine-learning-services.md)

## [아키텍처](python/architecture-overview-sql-server-python.md)
### [Python 상호 운용성](python/python-interoperability.md)
### [Python을 지원하는 구성 요소](python/new-components-in-sql-server-to-support-python-integration.md)
### [Python 보안](python/security-overview-sql-server-python-services.md)
## [모니터링](python/managing-and-monitoring-python-solutions.md)
<!-- ### [How To Create a Resource Pool for Python](python/how-to-create-a-resource-pool-for-python.md)-->
<!-- ### [Extended Events for Python](python/extended-events-for-python.md)-->
<!-- ### [DMVs for Python](python/dmvs-for-python.md)-->
<!-- ### [Resource Governance for Python](python/resource-governance-for-python.md)-->

## [Python 자습서](tutorials/sql-server-python-tutorials.md)

### [Python: T-SQL을 사용하여 Python 실행](tutorials/run-python-using-t-sql.md)
#### [저장 프로시저에서 Python 래핑](tutorials/wrap-python-in-tsql-stored-procedure.md)
#### [SQL Server의 Python 모델에서 학습 및 점수 매기기](tutorials/train-score-using-python-in-tsql.md)
#### [SQL Server 계산 컨텍스트에서 revoscalepy를 사용하여 모델 만들기](tutorials/use-python-revoscalepy-to-create-model.md)

### [Python: SQL 개발자를 위한 데이터베이스 내 분석](tutorials/sqldev-in-database-python-for-sql-developers.md)

#### [예제 데이터 다운로드](tutorials/sqldev-py1-download-the-sample-data.md)
#### [SQL Server로 데이터 가져 오기](tutorials/sqldev-py2-import-data-to-sql-server-using-powershell.md)
#### [데이터 탐색 및 시각화](tutorials/sqldev-py3-explore-and-visualize-the-data.md)
#### [T-SQL을 사용하여 데이터 기능 만들기](tutorials/sqldev-py4-create-data-features-using-t-sql.md)
#### [모델 학습 및 저장](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)
#### [모델 운영화](tutorials/sqldev-py6-operationalize-the-model.md)

# [Machine Learning Server - 독립 실행형](r/r-server-standalone.md)
## [시작](r/getting-started-with-microsoft-r-server-standalone.md)
## [독립 실행형 Machine Learning Server 설정](r/create-a-standalone-r-server.md)
### [명령줄에서 Microsoft Machine Learning Server 설치](r/install-microsoft-r-server-from-the-command-line.md)
### [데이터 과학 가상 컴퓨터 프로비저닝](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

# [방법](r/sql-server-machine-learning-tasks.md)

## [SQL Server에 대한 R 패키지 관리](r/r-package-management-for-sql-server-r-services.md)

### [SQL Server에 새로운 R 패키지 설치](r/install-additional-r-packages-on-sql-server.md)

### [SQL Server에 새로운 Python 패키지 설치](python/install-additional-python-packages-on-sql-server.md)

### [SQL Server 인스턴스에 대해 R 패키지 관리 사용](r/r-package-how-to-enable-or-disable.md)

### [SQL Server에 설치된 패키지 확인](r/determine-which-packages-are-installed-on-sql-server.md)

### [SQL Server에서 RevoScaleR 함수를 사용하여 R 패키지 찾기 또는 설치](r/use-revoscaler-to-manage-r-packages.md)

### [SQL Server에 설치된 R 패키지 동기화](r/package-install-uninstall-and-sync.md)

### [SQL Server에 설치된 R 패키지](r/installing-and-managing-r-packages.md)

### [miniCRAN을 사용하여 로컬 패키지 리포지토리 만들기](r/create-a-local-package-repository-using-minicran.md)

### [R에 대한 사용자 패키지 라이브러리의 오류 방지](r/packages-installed-in-user-libraries.md)

## 데이터 탐색 및 모델링

### [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)
### [Python 라이브러리 및 데이터 형식](python/python-libraries-and-data-types.md)
### [네이티브 점수 매기기](sql-native-scoring.md)
### [실시간 점수 매기기](real-time-scoring.md)
### [R을 이용한 예측 모델링](r/data-exploration-and-predictive-modeling-with-r.md)
### [실시간 또는 네이티브 점수 매기기를 수행하는 방법](r/how-to-do-realtime-scoring.md)
### [ODBC를 사용하여 R 개체 로드](r/save-and-load-r-objects-from-sql-server-using-odbc.md)
### [Machine Learning Services에서 사용하기 위해 R 코드 변환](r/converting-r-code-for-use-in-sql-server.md)
### [rxExecBy를 사용하여 여러 모델 만들기](r/creating-multiple-models-using-rxexecby.md)
### [미리 학습된 모델 설치](r/install-pretrained-models-sql-server.md)
### [R에서 OLAP 큐브의 데이터 사용](r/using-data-from-olap-cubes-in-r.md)
### [sqlrutils를 사용하여 저장 프로시저 만들기](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## 성능

### [R의 성능 튜닝 - 개요](r/sql-server-r-services-performance-tuning.md)
### [R의 성능 튜닝 - SQL Server 구성)](r/sql-server-configuration-r-services.md)
### [R의 성능 튜닝 - R 및 데이터 최적화](r/r-and-data-optimization-r-services.md)
### [R의 성능 튜닝 - 결과](r/performance-case-study-r-services.md)
### [R 코드 프로파일링 함수 사용](r/using-r-code-profiling-functions.md)


## 관리

### [R 구성 및 관리](r/configuration-sql-server-r-services.md)
### [Machine Learning Services의 고급 구성 옵션](r/configure-and-manage-advanced-analytics-extensions.md)
### [SQL Server의 R 런타임에 대한 보안 고려 사항](r/security-considerations-for-the-r-runtime-in-sql-server.md)
### [SQL Server Machine Learning Services의 사용자 계정 풀 수정](r/modify-the-user-account-pool-for-sql-server-r-services.md)

### [SQLRUserGroup을 데이터베이스 사용자로 추가](r/add-sqlrusergroup-to-database.md)

### [웹 서비스를 사용하여 모델 배포 및 사용](operationalization-with-mrsdeploy.md)

### [기계 학습 솔루션 관리 및 모니터링](r/managing-and-monitoring-r-solutions.md)
### [Machine Learning Services를 위한 리소스 거버넌스](r/resource-governance-for-r-services.md)
### [기계 학습을 위한 리소스 풀 만들기](r/how-to-create-a-resource-pool-for-r.md)
### [Machine Learning Services를 위한 확장 이벤트](r/extended-events-for-sql-server-r-services.md)
### [PREDICT 문 모니터링에 대한 확장 이벤트](xe-event-predict-tsql.md)
### [Machine Learning Services용 DMV](r/dmvs-for-sql-server-r-services.md)
### [R 코드 프로파일링 함수 사용](r/using-r-code-profiling-functions.md)
### [Management Studio에서 사용자 지정 보고서를 사용하여 Machine Learning Services 모니터링](r/monitor-r-services-using-custom-reports-in-management-studio.md)

# 리소스

## [알려진 문제](known-issues-for-sql-server-machine-learning-services.md)
## [릴리스 정보](https://docs.microsoft.com/sql/sql-server/sql-server-2017-release-notes)
## [새로운 또는 업데이트 된 문서](new-updated-advanced-analytics.md)
## [Azure SQL Database에서 R 사용](r/using-r-in-azure-sql-database.md)

## [설치 및 문제 해결 팁](machine-learning-troubleshooting-faq.md)
### [문제 해결을 위한 데이터 컬렉션](data-collection-ml-troubleshooting-process.md)
### [업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

### [외부 스크립트 실행에 대한 일반적인 문제](common-issues-external-script-execution.md)
### [인터넷에 액세스하지 않고 기계 학습 구성 요소 설치](r/installing-ml-components-without-internet-access.md)
### [Azure 가상 컴퓨터에 SQL Server Machine Learning Services 설치](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)
### [기존 Azure 가상 컴퓨터에 R 추가](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)
### [sqlBindR.exe를 사용하여 인스턴스 업그레이드](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
### [명령줄에서 R Server 설치](r/install-microsoft-r-server-from-the-command-line.md)
### [엔터프라이즈 데이터 과학 가상 컴퓨터 프로비전](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
### [데이터 과학 도구 설정](r/setup-or-configure-r-tools.md)
### [데이터 과학 클라이언트 설정](r/set-up-a-data-science-client.md)

## 블로그

### [SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/)
### [R Server](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/)
### [Machine Learning](https://blogs.technet.microsoft.com/machinelearning/)

## 피드백 포럼
### [SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver)
### [Microsoft R Server](https://social.msdn.microsoft.com/Forums/home?forum=MicrosoftR)

# [참조](r/machine-learning-services-r-reference.md)
## [MicrosoftML](using-the-microsoftml-package.md)
## [RevoScaleR](r/revoscaler-overview.md)
### [SQL Server 데이터를 위한 ScaleR 함수](r/scaler-functions-for-working-with-sql-server-data.md)
## [SqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
## [OlapR](r/how-to-create-mdx-queries-using-olapr.md)
## [RevoScalePy](python/what-is-revoscalepy.md)

# [자습서 및 예제](tutorials/machine-learning-services-tutorials.md)

## [SQL Server용 Python 자습서](tutorials/sql-server-python-tutorials.md)
## [SQL Server용 R 자습서](tutorials/sql-server-r-tutorials.md)

## [데이터 과학 솔루션 템플릿](tutorials/data-science-scenarios-and-solution-templates.md)
## [SQL Server 예제](https://github.com/Microsoft/sql-server-samples)

