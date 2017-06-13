## <a name="managing-synchronous-commit-mode"></a>동기 커밋 모드 관리

>[!WARNING]
>경우에 따라 Linux에서 동기 커밋 모드의 SQL Server 가용성 그룹은 데이터 손실에 취약할 수 있습니다. 데이터 손실을 방지하려면 근본 원인 및 해결 방법에 대한 다음 정보를 참조하세요. 이 문제는 이후 릴리스에서 해결될 예정입니다.

###<a name="pacemaker-notification-for-availability-group-resource-promotion"></a>가용성 그룹 리소스 승격에 대한 Pacemaker 알림

CTP 1.4 릴리스 이전에는 가용성 그룹의 Pacemaker 리소스 에이전트는 `SYNCHRONOUS_COMMIT`으로 표시된 복제본이 실제로 최신 상태인지 여부를 알 수 없었습니다. 복제본이 주 복제본과의 동기화를 중지했을 수 있으나 알 수 없었습니다. 따라서 에이전트는 오래된 복제본을 주 복제본으로 승격할 수 있었습니다. 성공할 경우 데이터 손실이 발생합니다. 

추가 하는 SQL Server 2017 CTP 1.4 `sequence_number` 를 `sys.availability_groups` 이 문제를 해결 하 합니다. `sequence_number`는 로컬 AG 복제본이 나머지 시스템을 기준으로 얼마나 최신 상태인지를 나타내는 단조롭게 증가하는 BIGINT입니다. 장애 조치(failover)를 수행하거나, 복제본을 추가/제거하거나, 기타 AG 작업을 수행하면 이 숫자가 업데이트됩니다. 이 숫자는 주 복제본에서 업데이트되고 보조 복제본으로 밀어넣어집니다. 따라서 최신 상태인 보조 복제본에는 주 복제본과 같은 숫자가 포함됩니다.

Pacemaker는 복제본을 주 복제본으로 승격하기로 결정하면 먼저 일련 번호를 추출하고 저장하도록 모든 복제본에 알림을 보냅니다. 그 다음에 Pacemaker가 실제로 복제본을 주 복제본으로 승격하려고 하면 일련 번호가 모든 일련 번호 중 가장 높을 경우 해당 복제본만 승격되고 이외의 경우에는 승격 작업이 거부됩니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다.

승격할 수 있는 하나 이상의 복제본에 이전 주 복제본과 같은 일련 번호가 있어야 이 방법을 적용할 수 있습니다. 리소스 에이전트의 경우 Pacemaker가 모든 복제본에 알림을 보내야 하므로 `notify=true`를 사용하여 가용성 리소스를 구성해야 합니다. 모든 기존 `ocf:mssql:ag` 리소스의 경우 사용자는 `mssql-server-ha` 패키지를 CTP 1.4로 업데이트하기 전에 `notify=true`를 사용하여 리소스 구성을 업데이트해야 합니다. 그렇지 않으면 리소스가 오류 상태로 전환됩니다. 

### <a name="how-to-avoid-potential-for-data-loss"></a>데이터 손실을 방지하는 방법 

다음과 같은 경우에도 가용성 그룹은 데이터 손실에 취약할 수 있습니다. 5개 노드가 포함된 클러스터에서 SQL Server의 세 개의 인스턴스에 복제본이 있는 가용성 그룹이 있으면 주 복제본 및 하나의 보조 복제본이 다른 보조 복제본보다 앞에 있을 수 있습니다. 앞에 있는 경우 `sys.availability_groups`의 `sequence_number`는 다른 복제본보다 더 높습니다. 이 조건에서 두 개의 복제본이 나머지 클러스터와 연결이 끊어지면 Pacemaker는 나머지 세 개의 노드를 쿼럼으로 확인하고 잠재 복제본이 주 복제본으로 승격되도록 허용합니다. 이 경우에는 데이터가 손실될 수 있습니다.

sql2017 주 서버에서 모든 트랜잭션을 커밋할 수 전에 사용 가능 하도록 보조 복제본의 특정 수를 강제 적용 하는 새 기능이 도입 되었습니다. `REQUIRED_COPIES_TO_COMMIT`을 사용하여 트랜잭션을 진행하기 전에 보조 복제본 데이터베이스 트랜잭션 로그로 커밋되어야 하는 많은 복제본을 설정할 수 있습니다. 이 옵션은 `CREATE AVAILABILITY GROUP` 또는 `ALTER AVAILABILITY GROUP`과 함께 사용할 수 있습니다. [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx)을 참조하세요.

위에 설명된 데이터 손실을 방지하려면 `REQUIRED_COPIES_TO_COMMIT`을 최대 개수의 동기화된 복제본으로 설정합니다. 이후 릴리스에서 `REQUIRED_COPIES_TO_COMMIT` 설정을 자동으로 처리하는 논리가 기본 제공될 예정입니다.
`REQUIRED_COPIES_TO_COMMIT`이 설정되면 주 복제본 데이터베이스의 트랜잭션은 필요한 개수의 동기 보조 복제본 데이터베이스 트랜잭션 로그에 커밋될 때까지 대기합니다. 충분한 동기 보조 복제본이 온라인 상태가 아니면 충분한 보조 복제본과의 통신이 다시 시작될 때까지 트랜잭션이 중지됩니다.

다음 예제에서는 가용성 그룹 이름 [ag1]을 `REQUIRED_COPIES_TO_COMMIT = 2`로 설정합니다. 

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1]
SET (REQUIRED_COPIES_TO_COMMIT = 2)
```

위의 예제에서 가용성 그룹에 두 개의 보조 복제본이 있으면 트랜잭션은 보조 복제본 승인이 커밋될 때까지 대기합니다. 하나라도 응답이 없으면 트랜잭션이 차단됩니다.
