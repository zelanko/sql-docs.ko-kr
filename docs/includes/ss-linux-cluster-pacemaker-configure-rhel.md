3. 모든 클러스터 노드에서 Pacemaker 방화벽 포트를 엽니다. `firewalld`를 사용하여 이러한 포트를 열려면 다음 명령을 실행합니다.

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 방화벽에 고가용성 구성이 기본 제공되지 않는 경우 Pacemaker에 대해 다음 포트를 엽니다.
   >
   > * TCP: 포트 2224, 3121, 21064
   > * UDP: 포트 5405

1. 모든 노드에 Pacemaker 패키지를 설치합니다.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 모든 노드에서 동일한 암호를 사용 합니다. 

   ```bash
   sudo passwd hacluster
   ```

3. 다시 부팅 후 노드가 클러스터에 다시 조인할 수 있도록 `pcsd` 서비스 및 Pacemaker를 사용하도록 설정하고 시작합니다. 모든 노드에서 다음 명령을 실행 합니다.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 클러스터를 만듭니다. 클러스터를 만들려면 다음 명령을 실행합니다.

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >이전에 같은 노드에서 클러스터를 구성한 경우 `pcs cluster setup`을 실행할 때 `--force` 옵션을 사용해야 합니다. 이 옵션은 `pcs cluster destroy`를 실행하는 것과 동일합니다. Pacemaker를 다시 사용하도록 설정하려면 `sudo systemctl enable pacemaker`를 실행합니다.

5. SQL Server용 SQL Server 리소스 에이전트를 설치합니다. 모든 노드에서 다음 명령을 실행 합니다. 

   ```bash
   sudo yum install mssql-server-ha
   ```
