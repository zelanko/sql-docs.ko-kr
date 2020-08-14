
<!--
### Code examples for Azure cloud differ slightly from on-premises
  Or.....
### Code examples can differ for Azure SQL Database
-->

SQL Server 온-프레미스용으로 작성된 일부 Transact-SQL 코드 예제를 클라우드의 Azure SQL Database 서비스에서 실행하려면 몇 가지 사항을 변경해야 합니다. 해당 코드 예제의 한 가지 범주로 두 데이터베이스 시스템에서 다음과 같이 이름 접두사에 약간 차이가 있는 시스템 뷰가 있습니다.

- **server\_** &nbsp; - &nbsp; ‘온-프레미스의 접두사’ 
- **database\_** &nbsp; - &nbsp; ‘Azure SQL Database의 접두사’

예시를 위해 다음 표에서는 시스템 뷰의 두 하위 집합을 나열하고 비교합니다. 알아보기 쉽도록 하위 집합은 `_event` 문자열을 포함하는 뷰 이름으로 제한되었습니다. 하위 집합은 각기 다른 두 데이터베이스 시스템에서 가져왔기 때문에 이름 접두사가 서로 다릅니다.

| 온-프레미스 2017의 이름 | 클라우드 서비스의 이름 |
| :------------------------- | :---------------------- |
| server_event_notifications<br />server_event_session_actions<br />server_event_session_events<br />server_event_session_fields<br />server_event_session_targets<br />server_event_sessions<br />server_events<br />server_trigger_events | database_event_session_actions<br />database_event_session_events<br />database_event_session_fields<br />database_event_session_targets<br />database_event_sessions |
| &nbsp; | &nbsp; |

위의 표에 나와 있는 두 목록은 2019년 6월을 기준으로 정확하게 표시되었습니다. 그러나 여기에 제공된 테이블 내용은 유지 관리되지 않으므로 만료될 수 있습니다. 정확한 목록을 보려면 다음 T-SQL SELECT 문을 실행합니다. 각 데이터베이스 시스템에서 한 번씩, SELECT를 두 번 실행합니다.

```sql
SELECT name
    FROM sys.all_objects
    WHERE
        (name LIKE 'database\_%' { ESCAPE '\' } OR
         name LIKE 'server\_%' { ESCAPE '\' })
        AND name LIKE '%\_event%' { ESCAPE '\' }
        AND type = 'V'
    ORDER BY name;
```

<!--
The creation of this docs/includes/ file was prompted by Issue 2211 (https://github.com/MicrosoftDocs/sql-docs/issues/2211).
Initial PR was PR 10427 (https://github.com/MicrosoftDocs/sql-docs-pr/pull/10427).
The complaint was that a specific T-SQL code block failed on Azure SQL Database.

GeneMi  ,  2019/05/28
-->
