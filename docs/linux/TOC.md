# [Linux의 SQL Server 정보](sql-server-linux-overview.md)

# 개요
## [릴리스 정보](sql-server-linux-release-notes.md)
## [이 릴리스의 새로운 기능](sql-server-linux-whats-new.md)
## [새로운 또는 업데이트 된 문서](new-updated-linux.md)
## [버전 및 지원되는 기능](sql-server-linux-editions-and-components-2017.md)

# 빠른 시작
## [설치 및 연결 - Red Hat](quickstart-install-connect-red-hat.md)
## [설치 및 연결 - SUSE](quickstart-install-connect-suse.md)
## [설치 및 연결 - Ubuntu](quickstart-install-connect-ubuntu.md)
## [실행 및 연결 - Docker](quickstart-install-connect-docker.md)
## [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
## [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

# 자습서
## [1_Windows에서 마이그레이션](sql-server-linux-migrate-restore-database.md)
## [2_Oracle에서 마이그레이션](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)
## [3_Docker에서 마이그레이션](tutorial-restore-backup-in-sql-server-container.md)
## [4_작업 만들기](sql-server-linux-run-sql-server-agent-job.md)
## [5_AD 인증 설정](sql-server-linux-active-directory-authentication.md)
## [6_장애 조치(Failover) 클러스터 인스턴스 만들기](sql-server-linux-shared-disk-cluster-configure.md)
### [iSCSI](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
### [NFS](sql-server-linux-shared-disk-cluster-configure-nfs.md)
### [SMB](sql-server-linux-shared-disk-cluster-configure-smb.md)
## [7_Pacemaker 클러스터 배포](sql-server-linux-deploy-pacemaker-cluster.md)
## [8_가용성 그룹 생성 및 구성](sql-server-linux-create-availability-group.md)
## [9_고가용성을 위해 Kubernetes에서 구성](tutorial-sql-server-containers-kubernetes.md)

# 개념
## Install
### [SQL Server 설치](sql-server-linux-setup.md)
### [SQL Server 도구 설치](sql-server-linux-setup-tools.md)
### [SQL Server 에이전트 설치](sql-server-linux-setup-sql-agent.md)
### [SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md)
### [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
### [GA 리포지토리 등록](sql-server-linux-change-repo.md)

## 구성
### [mssql-conf를 사용하여 구성](sql-server-linux-configure-mssql-conf.md)
### [환경 변수](sql-server-linux-configure-environment-variables.md)
### [Docker 컨테이너 구성](sql-server-linux-configure-docker.md)
### [고객 의견](sql-server-linux-customer-feedback.md)

## [개발](sql-server-linux-develop-overview.md)
### [연결 라이브러리](sql-server-linux-develop-connectivity-libraries.md)
### [Visual Studio Code 사용](sql-server-linux-develop-use-vscode.md)
### [SSMS 사용](sql-server-linux-develop-use-ssms.md)
### [SSDT 사용](sql-server-linux-develop-use-ssdt.md)

## [관리](sql-server-linux-management-overview.md)
### [SSMS를 사용하여 관리](sql-server-linux-manage-ssms.md)
### [PowerShell을 사용하여 관리](sql-server-linux-manage-powershell.md)
### [로그 전달 사용](sql-server-linux-use-log-shipping.md)
### [DB 메일 및 메일 알림 사용](sql-server-linux-db-mail-sql-agent.md)
### [가용성을 위해 다중 서브넷 구성](sql-server-linux-configure-multiple-subnet.md)

## [마이그레이션](sql-server-linux-migrate-overview.md)
### [Windows에서 BACPAC 내보내기 및 가져오기](sql-server-linux-migrate-ssms.md)
### [SQL Server Migration Assistant를 사용하여 마이그레이션](sql-server-linux-migrate-ssma.md)
### [bcp를 사용하여 대량 복사](sql-server-linux-migrate-bcp.md)

## [추출, 변환, 로드](sql-server-linux-migrate-ssis.md)
### [제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md)
### [SSIS 구성](sql-server-linux-configure-ssis.md)
### [SSIS 패키지 예약](sql-server-linux-schedule-ssis-packages.md)

## [비즈니스 연속성 구성](sql-server-linux-business-continuity-dr.md)
### [가용성 기본 사항](sql-server-linux-ha-basics.md)
### [백업 및 복원](sql-server-linux-backup-and-restore-database.md)
#### [Virtual Device Interface - Linux](sql-server-linux-backup-vdi-specification.md)
### [장애 조치(Failover) 클러스터 인스턴스](sql-server-linux-shared-disk-cluster-concepts.md)
#### [Red Hat Enterprise Linux(RHEL)]()
##### [구성(HA 추가 기능)](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)
##### [운영(HA 추가 기능)](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
#### [SUSE Linux Enterprise Server(SLES)]()
##### [구성(HA 추가 기능)](sql-server-linux-shared-disk-cluster-sles-configure.md)
### [가용성 그룹](sql-server-linux-availability-group-overview.md)
#### [고가용성을 위해 만들기](sql-server-linux-availability-group-ha.md)
##### [AG 구성](sql-server-linux-availability-group-configure-ha.md)
##### [RHEL에서 구성](sql-server-linux-availability-group-cluster-rhel.md)
##### [SLES에서 구성](sql-server-linux-availability-group-cluster-sles.md)
##### [Ubuntu에서 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
##### [운영](sql-server-linux-availability-group-failover-ha.md)
#### [읽기 배율 전용으로 만들기]()
##### [AG 구성](sql-server-linux-availability-group-configure-rs.md)

## [보안](sql-server-linux-security-overview.md)
### [보안 기능 시작](sql-server-linux-security-get-started.md)
### [연결 암호화](sql-server-linux-encrypted-connections.md)

## 성능
### [모범 사례](sql-server-linux-performance-best-practices.md)
### [성능 기능 시작](sql-server-linux-performance-get-started.md)

# 샘플
## 무인 설치
### [Red Hat Enterprise Linux(RHEL)](sample-unattended-install-redhat.md)
### [SUSE Linux Enterprise Server(SLES)](sample-unattended-install-suse.md)
### [Ubuntu](sample-unattended-install-ubuntu.md)

# 리소스
## [FAQ](sql-server-linux-faq.md)
## [문제 해결](sql-server-linux-troubleshooting-guide.md)
## [SQL Server 설명서](../sql-server/sql-server-technical-documentation.md)
## 파트너
### [모니터링](../sql-server/partner-monitor-sql-server.md)
### [고가용성 및 재해 복구](../sql-server/partner-hadr-sql-server.md)
### [관리](../sql-server/partner-management-sql-server.md)
### [개발](../sql-server/partner-dev-sql-server.md)
## [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/sql-server)
## [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
## [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)
## [Reddit](https://www.reddit.com/r/SQLServer)
