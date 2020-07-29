---
title: 저장 프로시저 호출(OLE DB) | Microsoft Docs
description: 저장 프로시저 호출(OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [OLE DB Driver for SQL Server], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7835af6a0e0cb42d63dd6670e863d3c0aea28d44
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012751"
---
# <a name="stored-procedures---calling"></a>저장 프로시저 - 호출
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  저장 프로시저는 0개 이상의 매개 변수를 가질 수 있으며 값을 반환할 수도 있습니다. OLE DB Driver for SQL Server를 사용할 때 저장 프로시저에 대한 매개 변수는 다음 방법을 통해 전달할 수 있습니다.  
  
-   데이터 값을 하드 코딩합니다.  
  
-   매개 변수 표식(?)을 사용하여 매개 변수를 지정하고, 프로그램 변수를 매개 변수 표식에 바인딩한 후 데이터 값을 프로그램 변수에 넣습니다.  
  
> [!NOTE]  
>  OLE DB로 명명된 매개 변수를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저를 호출할 때 매개 변수 이름은 '\@' 문자로 시작해야 합니다. 이는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에만 적용되는 제한 사항입니다. OLE DB Driver for SQL Server는 MDAC보다 더 엄격하게 이 제한 사항을 적용합니다.  
  
 매개 변수 지원을 위해 **ICommandWithParameters** 인터페이스가 명령 개체에 표시됩니다. 매개 변수를 사용하려면 소비자는 먼저 **ICommandWithParameters::SetParameterInfo** 메서드를 호출하거나 **GetParameterInfo** 메서드를 호출하는 호출 문을 통해 공급자에게 매개 변수를 설명합니다. 그런 다음 소비자는 버퍼의 구조를 지정하는 접근자를 만들고 매개 변수 값을 이 버퍼에 넣습니다. 마지막으로 소비자는 접근자의 핸들과 버퍼에 대한 포인터를 **Execute**로 전달합니다. 이후의 **Execute**에 대한 호출에서 소비자는 버퍼에 새 매개 변수 값을 넣고 접근자 핸들과 버퍼 포인터를 사용하여 **Execute**를 호출합니다.  
  
 매개 변수를 사용하여 임시 저장 프로시저를 호출하는 명령은 먼저 **ICommandWithParameters::SetParameterInfo**를 호출하여 매개 변수 정보를 정의해야 명령을 성공적으로 준비할 수 있습니다. 이는 임시 저장 프로시저의 내부 이름이 클라이언트에서 사용하는 외부 이름과 다르고, MSOLEDBSQL은 임시 저장 프로시저에 대한 매개 변수 정보를 확인하기 위해 시스템 테이블을 쿼리할 수 없기 때문입니다.  
  
 다음은 매개 변수 바인딩 프로세스의 단계입니다.  
  
1.  DBPARAMBINDINFO 구조의 배열에 매개 변수 정보, 즉 매개 변수 이름, 매개 변수의 데이터 형식에 대한 공급자별 이름 또는 표준 데이터 형식 이름 등을 채웁니다. 배열의 각 구조는 하나의 매개 변수를 설명합니다. 이 배열은 **SetParameterInfo** 메서드로 전달됩니다.  
  
2.  **ICommandWithParameters::SetParameterInfo** 메서드를 호출하여 공급자에게 매개 변수를 설명합니다. **SetParameterInfo**는 각 매개 변수의 네이티브 데이터 형식을 지정합니다. **SetParameterInfo** 인수는 다음과 같습니다.  
  
    -   형식 정보를 설정할 매개 변수의 수  
  
    -   형식 정보를 설정할 매개 변수 서수의 배열  
  
    -   DBPARAMBINDINFO 구조의 배열  
  
3.  **IAccessor::CreateAccessor** 명령을 사용하여 매개 변수 접근자를 만듭니다. 이 접근자는 버퍼의 구조를 지정하고 매개 변수 값을 버퍼에 넣습니다. **CreateAccessor** 명령은 바인딩 집합으로부터 접근자를 만듭니다. 이러한 바인딩은 소비자가 DBBINDING 구조의 배열을 사용하여 설명합니다. 각 바인딩은 단일 매개 변수를 소비자의 버퍼에 연결하며 다음과 같은 정보를 포함합니다.  
  
    -   바인딩이 적용되는 매개 변수의 서수  
  
    -   바인딩 대상(데이터 형식, 길이 및 상태)  
  
    -   이러한 각 부분에 대한 버퍼의 오프셋  
  
    -   소비자의 버퍼에 존재하는 데이터 값의 길이와 형식  
  
     접근자는 해당 핸들로 식별되며, 핸들은 HACCESSOR 형식입니다. 이 핸들은 **CreateAccessor** 메서드에 의해 반환됩니다. 소비자는 접근자 사용을 마칠 때마다 **ReleaseAccessor** 메서드를 호출하여 점유한 메모리를 해제해야 합니다.  
  
     소비자는 **ICommand::Execute**와 같은 메서드를 호출할 때 접근자에 대한 핸들과 버퍼 자체에 대한 포인터를 전달합니다. 공급자는 이 접근자를 사용하여 버퍼에 포함된 데이터를 전송할 방법을 확인합니다.  
  
4.  DBPARAMS 구조를 채웁니다. 입력 매개 변수 값이 읽히고 출력 매개 변수 값이 기록되는 소비자 변수는 런타임에 DBPARAMS 구조로 **ICommand::Execute**에 전달됩니다. DBPARAMS 구조에는 다음 3개의 요소가 포함됩니다.  
  
    -   접근자 핸들에 의해 지정된 바인딩에 따라 공급자가 입력 매개 변수 데이터를 가져오고 출력 매개 변수 데이터를 반환하는 버퍼에 대한 포인터  
  
    -   버퍼에 있는 매개 변수 집합의 수  
  
    -   3단계에서 만든 접근자 핸들  
  
5.  **ICommand::Execute**를 사용하여 명령을 실행합니다.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>저장 프로시저 호출 방법  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 저장 프로시저를 실행할 때 OLE DB Driver for SQL Server는 다음을 지원합니다.  
  
-   ODBC CALL 이스케이프 시퀀스  
  
-   RPC(원격 프로시저 호출) 이스케이프 시퀀스  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 문  
  
### <a name="odbc-call-escape-sequence"></a>ODBC CALL 이스케이프 시퀀스  
 매개 변수 정보를 알 경우 **ICommandWithParameters::SetParameterInfo** 메서드를 호출하여 공급자에게 매개 변수를 설명합니다. 그렇지 않은 경우 저장 프로시저 호출에 ODBC CALL 구문을 사용하면 공급자는 도우미 함수를 호출하여 저장 프로시저 매개 변수 정보를 찾습니다.  
  
 매개 변수 정보(매개 변수 메타데이터)가 확실하지 않을 경우에는 ODBC CALL 구문을 사용하는 것이 좋습니다.  
  
 ODBC CALL 이스케이프 시퀀스를 사용한 프로시저 호출의 일반적인 구문은 다음과 같습니다.  
  
 {[ **?=** ]**call**_procedure\_name_[ **(** [*parameter*][ **,** [_parameter_]]... **)** ]}  
  
 다음은 그 예입니다.  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>RPC 이스케이프 시퀀스  
 RPC 이스케이프 시퀀스는 ODBC CALL의 저장 프로시저 호출 구문과 비슷합니다. 프로시저를 여러 번 호출한다면 저장 프로시저를 호출하는 3가지 방법 중 RPC 이스케이프 시퀀스가 가장 높은 성능을 제공합니다.  
  
 RPC 이스케이프 시퀀스를 사용하여 저장 프로시저를 실행할 경우 공급자는 ODBC CALL 구문에서와는 달리 매개 변수 정보를 확인하기 위한 어떠한 도우미 함수도 호출하지 않습니다. RPC 구문은 ODBC CALL 구문보다 간단하므로 명령이 구문 분석되는 시간이 더 빠르고 성능이 향상됩니다. 이 경우 **ICommandWithParameters::SetParameterInfo**를 실행하여 매개 변수 정보를 제공해야 합니다.  
  
 RPC 이스케이프 시퀀스에서는 반환 값이 있어야 합니다. 저장 프로시저가 값을 반환하지 않으면 서버는 기본적으로 0을 반환합니다. 또한 저장 프로시저에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서를 열 수 없습니다. 저장 프로시저는 암시적으로 준비되며 **ICommandPrepare::Prepare**에 대한 호출은 실패합니다. RPC 호출을 준비할 수 없기 때문에 열 메타데이터를 쿼리할 수 없습니다. 따라서 IColumnsInfo::GetColumnInfo 및 IColumnsRowset::GetColumnsRowset에서 DB_E_NOTPREPARED를 반환합니다.  
  
 모든 매개 변수 메타데이터를 알고 있다면 RPC 이스케이프 시퀀스를 사용하여 저장 프로시저를 실행하는 것이 좋습니다.  
  
 다음은 RPC 이스케이프 시퀀스를 사용한 저장 프로시저 호출의 예입니다.  
  
```  
{rpc SalesByCategory}  
```  
  
 RPC 이스케이프 시퀀스를 보여주는 샘플 애플리케이션은 [&#40;RPC 구문을 사용하여&#41; 저장 프로시저를 실행하고 반환 코드 및 출력 매개 변수를 처리&#40;OLE DB&#41;](../../oledb/ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md)를 참조하세요.  
  
### <a name="transact-sql-execute-statement"></a>Transact-SQL EXECUTE 문  
 저장 프로시저를 호출할 때는 [EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md) 문보다 ODBC CALL 이스케이프 시퀀스와 RPC 이스케이프 시퀀스가 더 일반적으로 사용됩니다. OLE DB Driver for SQL Server는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 RPC 메커니즘을 사용하여 명령 처리를 최적화합니다. 이 RPC 프로토콜은 서버에서 수행되는 매개 변수 처리와 문 구문 분석의 대부분을 제거하여 성능을 향상시킵니다.  
  
 다음은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE** 문의 예입니다.  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저](../../oledb/ole-db/stored-procedures.md)  
  
  
