## <a name="pacemakerNotify"></a>Pacemaker용 SQL Server 리소스 에이전트 이해

CTP 1.4 릴리스 이전에는 가용성 그룹의 Pacemaker 리소스 에이전트가 `SYNCHRONOUS_COMMIT`으로 표시된 복제본이 실제로 최신 상태인지 여부를 알 수 없었습니다. 복제본이 주 복제본과의 동기화를 중지했을 수 있으나 알 수 없었습니다. 따라서 에이전트는 오래된 복제본을 주 복제본으로 수준을 올릴 수 있었고, 성공할 경우 데이터 손실이 발생했습니다. 

SQL Server 2017 CTP 1.4는 `sequence_number`를 `sys.availability_groups`에 추가하여 이 문제를 해결했습니다. `sequence_number`는 로컬 가용성 그룹 복제본이 가용성 그룹의 나머지 복제본을 기준으로 얼마나 최신 상태인지를 나타내는 단조롭게 증가하는 BIGINT입니다. 장애 조치(failover)를 수행하거나, 복제본을 추가/제거하거나, 기타 가용성 그룹 작업을 수행하면 이 숫자가 업데이트됩니다. 이 숫자는 주 복제본에서 업데이트되고 보조 복제본으로 밀어넣어집니다. 따라서 최신 상태인 보조 복제본은 주 복제본과 sequence_number가 같습니다. 

Pacemaker는 복제본을 주 복제본으로 수준을 올리기로 결정하면 먼저 일련 번호를 추출하고 저장하도록 모든 복제본에 알림을 보냅니다(이 알림을 수준 올리기 전 알림이라고 함). 그다음에 Pacemaker가 실제로 복제본을 주 복제본으로 수준을 올리려고 하면, 일련 번호가 모든 복제본의 모든 일련 번호 중 가장 높을 경우 해당 복제본만 수준이 올라가고 그렇지 않을 경우 수준 올리기 작업이 거부됩니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다. 

승격할 수 있는 하나 이상의 복제본에 이전 주 복제본과 같은 일련 번호가 있어야 이 방법을 적용할 수 있습니다. 이를 위한 기본 동작으로 Pacemaker 리소스 에이전트는 하나 이상의 동기 커밋 보조 복제본이 최신 상태이고 자동 장애 조치(failover)의 대상이 될 수 있도록 `REQUIRED_COPIES_TO_COMMIT`을 자동 설정합니다. 각 모니터링 작업에서 `REQUIRED_COPIES_TO_COMMIT` 값은 ('동기 커밋 복제본 수'/2)로 계산됩니다(필요한 경우 업데이트됨). 그런 다음 장애 조치(failover) 시 리소스 에이전트가 수준 올리기 전 알림에 응답하여 복제본 중 하나를 주 복제본으로 수준을 올리려면 (`total number of replicas` - `required_copies_to_commit` 복제본)이 필요합니다. `sequence_number`가 가장 높은 복제본이 주 복제본으로 수준이 올라갑니다. 

예를 들어 가용성 그룹에 동기 복제본 3개(주 복제본 1개, 동기 커밋 보조 복제본 2개)가 있다고 가정합니다.

- `REQUIRED_COPIES_TO_COMMIT`은 3/2 = 1입니다.

- 수준 올리기 전 작업에 응답하는 필요한 복제본 수는 3 - 1 = 2개입니다. 따라서 2개 복제본이 최신 상태여야만 장애 조치(failover)가 트리거됩니다. 즉, 주 복제본이 중단되는 경우 보조 복제본 중 하나가 응답하지 않고 보조 복제본 중 하나만 수준 올리기 전 작업에 응답하는 경우 리소스 에이전트는 응답한 보조 복제본의 sequence_number가 가장 높다고 보장할 수 없고 장애 조치(failover)가 트리거되지 않습니다.

사용자는 기본 동작을 재정의하고 위와 같이 `REQUIRED_COPIES_TO_COMMIT`을 자동으로 설정하지 않도록 가용성 그룹 리소스를 구성할 수 있습니다.

>[!IMPORTANT]
>`REQUIRED_COPIES_TO_COMMIT`이 0이면 데이터가 손실될 위험이 있습니다. 주 복제본 중단이 발생할 때 리소스 에이전트는 장애 조치(failover)를 자동으로 트리거하지 않습니다. 사용자가 주 복제본이 복구될 때까지 기다릴지, 수동으로 장애 조치(failover)할지 결정해야 합니다.

`REQUIRED_COPIES_TO_COMMIT`을 0으로 설정하려면 다음을 실행합니다.

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

crm(SLES에서) 사용 시 해당 명령은 다음과 같습니다.

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

계산된 기본값으로 되돌리려면 다음을 실행합니다.

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>리소스 속성을 업데이트하면 모든 복제본이 중지되고 다시 시작됩니다. 즉, 주 복제본의 수준이 일시적으로 보조 복제본으로 내려간 다음 다시 수준이 올라가면서 일시적으로 쓰기를 사용할 수 없게 됩니다. REQUIRED_COPIES_TO_COMMIT의 새 값은 복제본이 다시 시작되어야만 설정되므로 pcs 명령 실행과 함께 즉시 설정되지 않습니다.

## <a name="balancing-high-availability-and-data-protection"></a>고가용성과 데이터 보호 사이의 균형 유지 

위의 기본 동작은 동기 복제본(주 + 보조)이 2개인 경우에도 적용됩니다. Pacemaker에서는 데이터 보호를 향상하기 위해 보조 복제본이 항상 최신 상태로 유지되도록 `REQUIRED_COPIES_TO_COMMIT = 1`을 기본 설정합니다.  

>[!WARNING]
>이 경우 보조 복제본의 계획되거나 계획되지 않은 중단으로 인해 주 복제본을 사용할 수 없게 될 위험성이 높아집니다. 사용자는 리소스 에이전트의 기본 동작을 변경하고 `REQUIRED_COPIES_TO_COMMIT`을 0으로 재정의할 수 있습니다.

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

재정의하면 리소스 에이전트는 `REQUIRED_COPIES_TO_COMMIT`의 새 설정을 사용하고 계산을 중지합니다. 따라서 사용자가 적절하게 수동으로 업데이트해야 합니다(예를 들어 복제본 수를 늘리는 경우).

다음 표에서는 여러 가용성 그룹 리소스 구성에서 주 또는 보조 복제본에 대한 중단의 결과를 설명합니다.

### <a name="availability-group---2-sync-replicas"></a>가용성 그룹 - 동기 복제본 2개

| |주 중단 |1개 보조 복제본 중단
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|사용자가 수동 장애 조치(FAILOVER)를 실행해야 합니다. <br>데이터 손실이 있을 수 있습니다.<br> 새 주 복제본은 읽기/쓰기입니다. |주 복제본은 읽기/쓰기이고, 데이터 손실 위험에 노출됩니다.
|`REQUIRED_COPIES_TO_COMMIT=1` * |클러스터가 장애 조치(FAILOVER)를 자동으로 실행합니다. <br>데이터가 손실되지 않습니다. <br> 이전 주 복제본이 복구되어 보조 복제본으로 가용성 그룹에 조인될 때까지 새 주 복제본이 모든 연결을 거부합니다. |보조 복제본이 복구될 때까지 주 복제본이 모든 연결을 거부합니다.

\*Pacemaker용 SQL Server 리소스 에이전트 기본 동작입니다.

### <a name="availability-group---3-sync-replicas"></a>가용성 그룹 - 동기 복제본 3개

| |주 중단 |1개 보조 복제본 중단
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|사용자가 수동 장애 조치(FAILOVER)를 실행해야 합니다. <br>데이터 손실이 있을 수 있습니다. <br>새 주 복제본은 읽기/쓰기입니다. |주 복제본은 읽기/쓰기입니다.
|`REQUIRED_COPIES_TO_COMMIT=1` * |클러스터가 장애 조치(FAILOVER)를 자동으로 실행합니다. <br>데이터가 손실되지 않습니다. <br>새 주 복제본은 읽기/쓰기입니다. |주 복제본은 읽기/쓰기입니다. 

\*Pacemaker용 SQL Server 리소스 에이전트 기본 동작입니다.