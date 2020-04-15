---
title: 확장 이벤트 로그의 진단 정보
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: aaa180c2-5e1a-4534-a125-507c647186ab
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd7b912ef214d71a56bbd2771ef2326b80643d5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303901"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>확장 이벤트 로그의 진단 정보 액세스
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 데이터 액세스 추적([데이터 액세스 추적](https://go.microsoft.com/fwlink/?LinkId=125805))은 연결 링 버퍼에서 연결 실패에 대한 진단 정보를 쉽게 얻을 수 있고 확장 이벤트 로그에서 애플리케이션 성능 정보를 쉽게 얻을 수 있도록 업데이트되었습니다.  
  
 확장 이벤트 로그를 읽는 방법에 대한 자세한 내용은 [View Event Session Data](https://msdn.microsoft.com/library/ac742a01-2a95-42c7-b65e-ad565020dc49)를 참조하십시오.  
  
> [!NOTE]  
>  이 기능은 문제 해결 및 진단 용도로만 제공되며 감사 또는 보안 용도에는 적합하지 않을 수 있습니다.  
  
## <a name="remarks"></a>설명  
 연결 작업의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 클라이언트 연결 ID를 전송합니다. 연결이 실패하는 경우 연결 링 버퍼에 액세스할 수 있으며([연결 링 버퍼가 있는 SQL Server 2008의 연결 문제 해결](https://go.microsoft.com/fwlink/?LinkId=207752)) **ClientConnectionID** 필드를 찾아서 연결 실패에 대한 진단 정보를 얻을 수 있습니다. 클라이언트 연결 ID는 오류가 발생하는 경우에만 링 버퍼에 기록됩니다. (prelogin 패킷을 보내기 전에 연결이 실패하면 클라이언트 연결 ID가 생성되지 않습니다.) 클라이언트 연결 ID는 16바이트 GUID입니다. 확장 이벤트 세션에서 **client_connection_id** 동작을 이벤트에 추가한 경우 확장 이벤트 출력 대상에서 클라이언트 연결 ID를 찾을 수도 있습니다. 추가 진단 지원이 필요한 경우 데이터 액세스 추적을 활성화하고 연결 명령을 다시 실행한 다음 실패한 작업에 대한 데이터 액세스 추적에서 **ClientConnectionID** 필드를 관찰할 수 있습니다.  
  
 네이티브 클라이언트에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC를 사용하고 있고 연결이 성공하면 [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)에서 **SQL_COPT_SS_CLIENT_CONNECTION_ID** 특성을 사용하여 클라이언트 연결 ID를 얻을 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 스레드별 작업 ID도 전송합니다. TRACK_CAUSAILITY 옵션이 활성화된 상태에서 세션을 시작한 경우 작업 ID는 확장 이벤트 세션에서 캡처됩니다. 활성 연결에 성능 문제가 발생할 경우 클라이언트의 데이터 액세스 추적(**ActivityID** 필드)에서 작업 ID를 가져온 다음 확장 이벤트 출력에서 작업 ID를 찾을 수 있습니다. 확장 이벤트의 작업 ID는 4바이트 시퀀스 번호가 추가된 16바이트 GUID(클라이언트 연결 ID의 GUID와 동일하지 않음)입니다. 시퀀스 번호는 스레드 내의 요청 순서를 나타내며 스레드에 대한 일괄 처리 및 RPC 문의 상대적인 순서를 표시합니다. 데이터 액세스 추적을 활성화하고 데이터 액세스 추적 구성 단어의 18번째 비트를 ON으로 전환하면 SQL 일괄 처리 문과 RPC 요청에 대해 **ActivityID** 가 선택적으로 전송됩니다.  
  
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
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 SQL Server Native Client 제어 파일(ctrl.guid.snac11)의 내용은 다음과 같습니다.  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x00000000  0   MSDADIAG.ETW  
{2DA81B52-908E-7DB6-EF81-76856BB47C4F}  0xFFFFFFFF  0   SQLNCLI11.1  
```  
  
## <a name="mof-file"></a>MOF 파일  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 SQL Server Native Client mof 파일의 내용은 다음과 같습니다.  
  
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
//  SQLNCLI11.1  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B52-908E-7DB6-EF81-76856BB47C4F}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B53-908E-7DB6-EF81-76856BB47C4F}"),  
 DisplayName("SQLNCLI11.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace : Bid2Etw_SQLNCLI11_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextA : Bid2Etw_SQLNCLI11_1_Trace  
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
 Description("SQLNCLI11.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextW : Bid2Etw_SQLNCLI11_1_Trace  
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
 [오류 및 메시지 처리](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
