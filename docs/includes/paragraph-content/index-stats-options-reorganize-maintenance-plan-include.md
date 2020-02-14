

### <a name="index-stats-options"></a>인덱스 통계 옵션

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


이전 버전의 Microsoft SQL Server에서 큰 인덱스를 다시 구성하거나 다시 작성하기 위해 시스템 속도가 느려지는 문제가 발생할 수 있습니다. SQL Server 2016는 이러한 인덱스 작업에 대한 주요 성능 향상을 구현했습니다.

또한 이전 버전에서는 컨트롤의 세분성이 덜 구체화되었습니다. 이로 인해 인덱스가 불필요하여 별로 조각화되지 않은 경우에도 시스템이 일부 인덱스를 다시 구성하거나 다시 작성하게 됩니다. 유지 관리 계획 사용자 인터페이스(UI)에서 최신 컨트롤을 사용하면 인덱스 통계 기준에 따라 새로 고칠 필요가 없는 인덱스를 제외할 수 있습니다. 다음과 같은 Transact-SQL의 동적 관리 뷰(DMVs)는 내부적으로 사용됩니다.


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **검색 유형**  
 이 시스템은 인덱스 통계를 수집하기 위해 리소스를 사용해야 합니다. 인덱스 통계에 얼마나 많은 자릿수가 필요한지에 따라, 상대적으로 더 많거나 적은 리소스 중에서 사용하도록 선택할 수 있습니다. 이 UI는 다음과 같은 전체 자릿수 목록을 제공하며 여기서 하나를 선택해야 합니다.


- 빠름
- 샘플링됨
- Detailed


 **다음 경우에만 인덱스 최적화:**  
 이 UI는 새로 고침이 아직 반드시 필요하지는 않은 경우 새로 고침 인덱스를 방지하는 데 사용할 수 있도록 다음과 같은 튜닝 필터를 제공합니다.


- 조각화 &gt; *(%)*
- 페이지 수 &gt;
- 지난 *일*간 사용됨

