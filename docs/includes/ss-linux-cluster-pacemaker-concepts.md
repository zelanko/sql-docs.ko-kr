## <a name="pacemakerNotify"></a>SQL Server 리소스 에이전트 pacemaker에 대 한 이해

1.4 CTP 릴리스 전에 가용성 그룹에 대 한 Pacemaker 리소스 에이전트 수 알 수 없습니다 복제본으로 표시 하는 경우 `SYNCHRONOUS_COMMIT` 는 실제로 최신 상태 인지 합니다. 복제본이 주 복제본과의 동기화를 중지했을 수 있으나 알 수 없었습니다. 따라서 에이전트가 성공적으로 실행 되는 데이터가 손실 되는 기본-오래 된 복제본을 승격할 수 없습니다. 

SQL Server 2017 CTP 1.4 추가 `sequence_number` 를 `sys.availability_groups` 이 문제를 해결 하 합니다. `sequence_number`가용성 그룹에 복제본의 나머지 부분에 대해 얼마나 최신 로컬 가용성 그룹 복제본이 나타내는 단조 증가 BIGINT입니다. 장애 조치를 수행, 추가 또는 제거 하는 복제본 및 다른 가용성 그룹 작업에는이 번호를 업데이트 합니다. 수는 주 서버, 업데이트 한 다음 보조 복제본에 전달 합니다. 따라서 최신 상태는 보조 복제본에 주 동일한 sequence_number를 갖습니다. 

시퀀스 번호를 추출 하 고 저장 하려면 모든 복제본에 알림을 Pacemaker를 주 복제본을 결정 하는 경우 먼저 보냅니다 (이 이라고는 미리 알림 승격). 다음으로 Pacemaker 실제로 주 복제본을 하려고 복제본만 승격 자체의 시퀀스 번호의 모든 복제본에서 모든 시퀀스 번호가 가장 높은 하 고 그렇지 않으면 수준 올리기 작업을 거부 합니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다. 

승격할 수 있는 하나 이상의 복제본에 이전 주 복제본과 같은 일련 번호가 있어야 이 방법을 적용할 수 있습니다. 이 위해 기본 동작은 Pacemaker 리소스 에이전트가 자동으로 설정 하는 데 `REQUIRED_COPIES_TO_COMMIT` 복제본은 최신 하 고 자동 장애 조치 대상으로 사용할 수 있는 하나 이상의 동기 커밋 보조 되도록 합니다. 각 모니터링 작업의 값으로 `REQUIRED_COPIES_TO_COMMIT` 계산 (및 필요한 경우 업데이트)로 ('동기 커밋 복제본 중 number' / 2). 그런 다음 장애 조치 시 리소스 에이전트가 필요 합니다 (`total number of replicas`  -  `required_copies_to_commit` 복제본)에 응답 하는 미리 알림 주 데이터베이스에 둘 중 하나의 수준을 올릴 수를 승격 합니다. 순위가 가장 높은 복제본 `sequence_number` primary로 승격 됩니다. 

예를 들어 세 개의 동기 복제본-하나의 주 복제본과 두 개의 동기 커밋 보조 복제본이 포함 된 가용성 그룹의 경우를 살펴보겠습니다.

- `REQUIRED_COPIES_TO_COMMIT`3 / 2 = 1

- 필요한 수의 작업을 미리 승격에 응답 하는 복제본은 3-1 = 2입니다. 따라서 2 개의 복제본 시작 옵션으로 장애 조치에 대해 있어야 합니다. 즉, 기본 가동 중단의 경우 보조 복제본 중 하나를 응답 하지 않는 경우 보조 데이터베이스 중 하나에만 응답 하는 작업을 미리 승격 리소스 에이전트 응답 보조가 가장 높은 sequence_number 및 장애 조치는 트리거되지 않습니다 보장할 수 없습니다.

사용자는 기본 동작을 재정의 하 고 되지 않도록 설정 하는 가용성 그룹 리소스를 구성 하도록 선택할 수 `REQUIRED_COPIES_TO_COMMIT` 자동으로 위의 설명 참조 합니다.

>[!IMPORTANT]
>때 `REQUIRED_COPIES_TO_COMMIT` 0 위치는 데이터 손실의 위험 합니다. 주 가동 중단의 경우 리소스 에이전트가 자동으로 장애 조치를 트리거하지 않습니다. 사용자는 기본을 복구 또는 수동 장애 조치에 대 한 대기 것인지를 결정 해야 합니다.

설정 하려면 `REQUIRED_COPIES_TO_COMMIT` 0으로 실행 합니다.

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

기본적으로 되돌리려면 계산 된 값, 실행:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=
```

>[!NOTE]
>모든 복제본 중지 했다가 다시 시작 하면 리소스 속성을 업데이트 합니다. 이 즉, 기본 보조 강등 후 일시적으로 임시에서 쓸 사용 불가 다시 승격 됩니다. REQUIRED_COPIES_TO_COMMIT에 대 한 새 값만 설정 됩니다 복제본 다시 시작 되 고 나면 이므로 pc 명령을 실행 하 여 즉시 수 없습니다.

## <a name="balancing-high-availability-and-data-protection"></a>높은 가용성 및 데이터 보호를 균형 조정 

위의 기본 동작은 동기 2 개의 복제본 (주 + 보조)의 경우에도 적용 됩니다. 기본값은 pacemaker `REQUIRED_COPIES_TO_COMMIT = 1` 하려면 보조 복제본은 항상 최신 데이터를 최대한 보호에 대 한 합니다.  

>[!WARNING]
>이 보조 복제본에서 더 높은 위험 계획적 이거나 비계획적인 정전으로 인해 주 복제본의 가용성을 함께 제공 됩니다. 사용자 리소스 에이전트의 기본 동작을 변경 하 고 재정의 하도록 선택할 수는 `REQUIRED_COPIES_TO_COMMIT` 0으로:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

리소스 에이전트가 사용에 대 한 새 설정이 재정의 되 면 `REQUIRED_COPIES_TO_COMMIT` 및 계산을 중지 합니다. 이 수동 업데이트를 적절 하 게 (예를 들어 이러한 증가 하는 경우 복제본의 수) 사용자가을 의미 합니다.

다음 표에서 서로 다른 가용성 그룹 리소스 구성의 주 또는 보조 복제본에 대 한 중단의 결과를 설명 합니다.

### <a name="availability-group---2-sync-replicas"></a>가용성 그룹-동기화 복제본 2 개

| |기본 중단 |하나의 보조 복제본의 작동 중단
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|사용자가 수동 장애 조치를 실행 합니다. <br>데이터 손실이 있을 수 있습니다.<br> 새 주 파일 그룹은 읽기/쓰기 |기본은 R/W, 데이터 손실에 노출 실행
|`REQUIRED_COPIES_TO_COMMIT=1` * |클러스터를 자동으로 장애 조치 발급 <br>데이터가 손실 되지 않습니다. <br> 새로운 주 이전의 주 복구 하 고 보조 복제본으로 가용성 그룹에 조인 될 때까지 모든 연결을 거부 합니다. |기본에서 보조 복구 될 때까지 모든 연결을 거부 합니다.

\*Pacemaker 기본 동작에 대 한 SQL Server 리소스 에이전트입니다.

### <a name="availability-group---3-sync-replicas"></a>가용성 그룹-동기화 복제본 3 개

| |기본 중단 |하나의 보조 복제본의 작동 중단
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|사용자가 수동 장애 조치를 실행 합니다. <br>데이터 손실이 있을 수 있습니다. <br>새 주 파일 그룹은 읽기/쓰기 |주 파일 그룹은 읽기/쓰기
|`REQUIRED_COPIES_TO_COMMIT=1` * |클러스터 장애 조치를 자동으로 발급 됩니다. <br>데이터가 손실 되지 않습니다. <br>새 주 파일 그룹은 RW |주 파일 그룹은 읽기/쓰기 

\*Pacemaker 기본 동작에 대 한 SQL Server 리소스 에이전트입니다.