---
title: 확장 이벤트 로그의 진단 정보 액세스 | Microsoft Docs
description: OLE DB Driver for SQL Server 추적 및 확장 이벤트 로그의 진단 정보 액세스
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96873ca61bd7121316d8b7d947443a90d7d953b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727334"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>확장 이벤트 로그의 진단 정보 액세스
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터 SQL Server용 OLE DB 드라이버와 데이터 액세스 추적([Data Access Tracing](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100)))은 연결 링 버퍼에서 연결 실패에 대한 진단 정보를 쉽게 얻을 수 있고 확장 이벤트 로그에서 애플리케이션 성능 정보를 쉽게 얻을 수 있도록 업데이트되었습니다.  
  
 확장 이벤트 로그를 읽는 방법에 대한 자세한 내용은 [View Event Session Data](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)를 참조하십시오. 

  
> [!NOTE]  
>  이 기능은 문제 해결 및 진단 용도로만 제공되며 감사 또는 보안 용도에는 적합하지 않을 수 있습니다.  
  
## <a name="remarks"></a>설명  
 연결 작업의 경우, OLE DB Driver for SQL Server에서 클라이언트 연결 ID를 전송합니다. 연결이 실패하는 경우 연결 링 버퍼에 액세스할 수 있으며([연결 링 버퍼가 있는 SQL Server 2008의 연결 문제 해결](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer) **ClientConnectionID** 필드를 찾아서 연결 실패에 대한 진단 정보를 얻을 수 있습니다. 클라이언트 연결 ID는 오류가 발생하는 경우에만 링 버퍼에 기록됩니다. 로그인 전 패킷을 전송하기 전에 연결이 실패하는 경우 클라이언트 연결 ID는 생성되지 않습니다. 클라이언트 연결 ID는 16바이트 GUID입니다. 확장 이벤트 세션에서 **client_connection_id** 동작을 이벤트에 추가한 경우 확장 이벤트 출력 대상에서 클라이언트 연결 ID를 찾을 수도 있습니다. 추가 진단 지원이 필요한 경우 데이터 액세스 추적을 활성화하고 연결 명령을 다시 실행한 다음 실패한 작업에 대한 데이터 액세스 추적에서 **ClientConnectionID** 필드를 관찰할 수 있습니다.  
   
  
 또한 OLE DB Driver for SQL Server는 스레드별 작업 ID를 전송합니다. TRACK_CAUSAILITY 옵션이 활성화된 상태에서 세션을 시작한 경우 작업 ID는 확장 이벤트 세션에서 캡처됩니다. 활성 연결에 성능 문제가 발생할 경우 클라이언트의 데이터 액세스 추적(**ActivityID** 필드)에서 작업 ID를 가져온 다음 확장 이벤트 출력에서 작업 ID를 찾을 수 있습니다. 확장 이벤트의 작업 ID는 4바이트 시퀀스 번호가 추가된 16바이트 GUID(클라이언트 연결 ID의 GUID와 동일하지 않음)입니다. 시퀀스 번호는 스레드 내의 요청 순서를 나타내며 스레드에 대한 일괄 처리 및 RPC 문의 상대적인 순서를 표시합니다. 데이터 액세스 추적을 활성화하고 데이터 액세스 추적 구성 단어의 18번째 비트를 ON으로 전환하면 SQL 일괄 처리 문과 RPC 요청에 대해 **ActivityID** 가 선택적으로 전송됩니다.  
  
 다음 예제에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 사용하여 링 버퍼에 저장되고 RPC 및 일괄 처리 작업 시 클라이언트에서 전송된 작업 ID를 기록하는 확장 이벤트 세션을 시작합니다.  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
  
```  
  
## <a name="control-file"></a>제어 파일  
 OLE DB Driver for SQL Server 제어 파일(ctrl.guid)의 내용은 다음과 같습니다.  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>MOF 파일  
 OLE DB Driver for SQL Server MOF 파일의 내용은 다음과 같습니다.  
  
```  
#pragma classflags("forceupdate")  
#pragma namespace ("\\\\.\\Root\\WMI")  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSDADIAG.ETW  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F3-3CC6-0B9C-6651-9649CCE5C752}"),  
 DisplayName("msdadiag"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace : Bid2Etw_MSDADIAG_ETW  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextA : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextW : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSOLEDBSQL.1  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59D-D3E8-9684-AEAC-B214EFD91B31}"),  
 DisplayName("MSOLEDBSQL.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace : Bid2Etw_MSOLEDBSQL_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextA : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextW : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
```  
  
## <a name="see-also"></a>참고 항목  
 [오류 처리](../../oledb/ole-db-errors/errors.md)  
  
