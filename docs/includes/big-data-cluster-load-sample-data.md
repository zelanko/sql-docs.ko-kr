### <a id="sampledata"></a> 샘플 데이터 로드

SQL Server 빅 데이터 클러스터 자습서에는 공용 샘플 데이터 집합을 사용합니다. 빅 데이터 클러스터에 샘플 데이터를 구성 하려면 다음 단계를 사용 합니다.

1. SQL Server 명령줄 도구가 없는 경우 (**sqlcmd** 하 고 **bcp**) 링크 중 하나를 사용 하 여 이러한 도구를 먼저 설치를 설치 합니다.

   * **Windows**: [Windows의 SQL Server 설치 명령줄 도구](https://www.microsoft.com/download/details.aspx?id=53591)
   * **Linux**: [Linux의 SQL Server 설치 명령줄 도구](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-tools)

1. 샘플 백업 파일을 다운로드 [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) 컴퓨터에 있습니다.

1. SQL Server 2019 빅 데이터 클러스터로 이동 [샘플 디렉터리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)합니다.

1. 다운로드 합니다 [부트스트랩-샘플-db.sql](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql) Transact SQL 스크립트.

1. 다운로드 하 고 명령줄에서 다음 두 가지 샘플 스크립트 중 하나를 실행 합니다.

   * **Windows**: [db.cmd-부트스트랩-샘플](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd)
   * **Linux**: [db.sh-부트스트랩-샘플](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh)

   > [!TIP]
   > 매개 변수 없이 스크립트를 실행 하 여 사용 지침을 얻을 수 있습니다.

마스터 SQL Server 인스턴스로 샘플 데이터베이스를 복원 하 고 또한 저장소 풀의 HDFS에 데이터를 로드 하는 스크립트.