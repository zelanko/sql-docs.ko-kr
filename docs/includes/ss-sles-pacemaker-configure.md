1. **두 클러스터 노드에서 모두 Pacemaker 로그인을 위한 SQL Server 사용자 이름 및 암호를 저장할 파일을 만듭니다.** 다음 명령은 이 파일을 만들고 채웁니다.

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **모든 클러스터 노드는 SSH를 통해 서로 액세스할 수 있어야 합니다**. hb_report 또는 crm_report(문제 해결용), Hawk의 History Explorer 등의 도구에는 노드 간에 암호 없는 SSH 액세스가 필요합니다. 그렇지 않으면 현재 노드에서만 데이터를 수집할 수 있습니다. 표준이 아닌 SSH 포트를 사용할 경우 -X 옵션을 사용합니다(기본 페이지 참조). 예를 들어 SSH 포트가 3479이면 함께 hb_report를 호출합니다.

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    자세한 내용은 [System Requirements and Recommendations in the SUSE documentation](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)(SUSE 설명서의 시스템 요구 사항 및 권장 사항)을 참조하세요.

3. **고가용성 확장을 설치합니다**. 확장을 설치하려면 다음 SUSE 항목의 단계를 따릅니다.
    
    [Installation and Setup Quick Start](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)(설치 및 설정 빠른 시작)

4. **SQL Server용 FCI 리소스 에이전트를 설치합니다**. 두 노드에서 모두 다음 명령을 실행합니다.

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **첫 번째 노드를 자동으로 설정합니다**. 다음 단계에서는 첫 번째 노드 SLES1을 구성하여 실행 중인 단일 노드 클러스터를 설정합니다. SUSE 항목 [Setting Up the First Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)(첫 번째 노드 설정)의 지침을 따릅니다.

    완료되면 `crm status`를 사용하여 클러스터 상태를 확인합니다.
    ```bash
    crm status
    ```

    단일 노드 SLES1이 구성된 것으로 표시됩니다.

6. **기존 클러스터에 노드를 추가합니다**. 그 다음에 SLES2 노드를 클러스터에 조인합니다. SUSE 항목 [Adding the Second Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node)(두 번째 노드 추가)의 지침을 따릅니다.
    
    완료되면 **crm status**를 사용하여 클러스터 상태를 확인합니다. 두 번째 노드를 성공적으로 추가한 경우 출력이 다음과 같이 표시됩니다.
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr**는 초기 단일 노드 클러스터 설정 중에 구성된 가상 IP 클러스터 리소스입니다.

7.  **제거 절차**. 클러스터에서 노드를 제거해야 할 경우 **ha-cluster-remove** 부트스트랩 스크립트를 사용합니다. 자세한 내용은 [Overview of the Bootstrap Scripts](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap)(부트스트랩 스크립트 개요)를 참조하세요.  

