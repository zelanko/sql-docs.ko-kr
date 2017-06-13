2. 모든 클러스터 노드에서 SQL Server 사용자 이름 및 Pacemaker 로그인 암호를 저장 하기 위해 파일을 만듭니다. 다음 명령은 이 파일을 만들고 채웁니다.

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 모든 클러스터 노드에서 Pacemaker 방화벽 포트를 엽니다. `firewalld`를 사용하여 이러한 포트를 열려면 다음 명령을 실행합니다.

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 기본 제공된 고가용성 구성이 없는 또 다른 방화벽을 사용 중인 경우 Pacemaker가 클러스터의 다른 노드와 통신할 수 있으려면 다음 포트를 열어야 합니다.
   >
   > * TCP: 포트 2224, 3121, 21064
   > * UDP: 포트 5405

1. 각 노드에 Pacemaker 패키지를 설치합니다.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 모든 노드에서 동일한 암호를 사용 합니다. 

   ```bash
   sudo passwd hacluster
   ```

   

3. `pcsd` 서비스 및 Pacemaker를 사용하도록 설정하고 시작합니다. 이렇게 하면 다시 시작된 후 노드가 클러스터에 다시 조인할 수 있습니다. 모든 노드에서 다음 명령을 실행 합니다.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. SQL Server용 FCI 리소스 에이전트를 설치합니다. 모든 노드에서 다음 명령을 실행 합니다. 

   ```bash
   sudo yum install mssql-server-ha
   ```
