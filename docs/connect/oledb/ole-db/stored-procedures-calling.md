---
title: 저장된 프로시저 (OLE DB) 호출 | Microsoft Docs
description: 저장 프로시저 호출(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d537b2f84bd59e24e25c54a61b14c549cef013da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="stored-procedures---calling"></a>저장된 프로시저-호출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  저장 프로시저는 0개 이상의 매개 변수를 가질 수 있으며 값을 반환할 수도 있습니다. OLE DB Driver for SQL Server를 사용할 때 매개 변수는 저장된 프로시저를 통해 전달할 수 있습니다.  
  
-   데이터 값을 하드 코딩합니다.  
  
-   매개 변수 표식(?)을 사용하여 매개 변수를 지정하고, 프로그램 변수를 매개 변수 표식에 바인딩한 후 데이터 값을 프로그램 변수에 넣습니다.  
  
> [!NOTE]  
>  OLE DB로 명명된 매개 변수를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저를 호출할 때 매개 변수 이름은 '@' 문자로 시작해야 합니다. 이는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에만 적용되는 제한 사항입니다. OLE DB Driver for SQL Server는 MDAC 보다 더 엄격 하 게이 제한을 적용합니다.  
  
 매개 변수를 지원 하기 위해는 **ICommandWithParameters** 인터페이스 명령 개체에서 노출 됩니다. 매개 변수를 사용 하려면 소비자는 먼저 매개 변수를 설명 공급자를 호출 하 여는 **icommandwithparameters:: Setparameterinfo** 메서드 (또는 필요에 따라 호출 하는 호출 문을 준비는 **GetParameterInfo** 메서드). 그런 다음 소비자는 버퍼의 구조를 지정하는 접근자를 만들고 매개 변수 값을 이 버퍼에 넣습니다. 버퍼에 대 한 포인터를 소비자는 접근자의 핸들 마지막으로, 전달 **Execute**합니다. 에 대 한 후속 호출에서 **Execute**, 소비자 버퍼 및 호출에 새 매개 변수 값을 배치 **Execute** 접근자 핸들과 버퍼 포인터입니다.  
  
 매개 변수를 사용 하 여 임시 저장된 프로시저를 호출 하는 명령은 먼저 호출 해야 **icommandwithparameters:: Setparameterinfo** 명령이 성공적으로 준비할 수 전에 매개 변수 정보를 정의할 수 있습니다. 이 임시 저장된 프로시저에 대 한 내부 이름이 클라이언트에서 사용 된 외부 이름에서 다른 MSOLEDBSQL 임시 저장된 프로시저에 대 한 매개 변수 정보를 확인 하는 시스템 테이블을 쿼리할 수 없습니다 때문입니다.  
  
 다음은 매개 변수 바인딩 프로세스의 단계입니다.  
  
1.  DBPARAMBINDINFO 구조의 배열에 매개 변수 정보, 즉 매개 변수 이름, 매개 변수의 데이터 형식에 대한 공급자별 이름 또는 표준 데이터 형식 이름 등을 채웁니다. 배열의 각 구조는 하나의 매개 변수를 설명합니다. 이 배열에 전달 되는 **SetParameterInfo** 메서드.  
  
2.  호출 된 **icommandwithparameters:: Setparameterinfo** 매개 변수는 공급자를 설명 하는 메서드. **SetParameterInfo** 각 매개 변수의 네이티브 데이터 형식을 지정 합니다. **SetParameterInfo** 인수가:  
  
    -   형식 정보를 설정할 매개 변수의 수  
  
    -   형식 정보를 설정할 매개 변수 서수의 배열  
  
    -   DBPARAMBINDINFO 구조의 배열  
  
3.  매개 변수 접근자를 사용 하 여 만들는 **iaccessor:: Createaccessor** 명령입니다. 이 접근자는 버퍼의 구조를 지정하고 매개 변수 값을 버퍼에 넣습니다. **CreateAccessor** 명령은 바인딩 집합에서 접근자를 만듭니다. 이러한 바인딩은 소비자가 DBBINDING 구조의 배열을 사용하여 설명합니다. 각 바인딩은 단일 매개 변수를 소비자의 버퍼에 연결하며 다음과 같은 정보를 포함합니다.  
  
    -   바인딩이 적용되는 매개 변수의 서수  
  
    -   바인딩 대상(데이터 형식, 길이 및 상태)  
  
    -   이러한 각 부분에 대한 버퍼의 오프셋  
  
    -   소비자의 버퍼에 존재하는 데이터 값의 길이와 형식  
  
     접근자는 해당 핸들로 식별되며, 핸들은 HACCESSOR 형식입니다. 이 핸들에서 반환 되는 **CreateAccessor** 메서드. 소비자는 접근자를 사용 하 여 완료 되 면 때마다 소비자 호출 해야 합니다는 **ReleaseAccessor** 메서드를 보유 하는 메모리를 해제 합니다.  
  
     소비자 호출 하는 경우 메서드를 같은 **icommand:: Execute**, 접근자 및 버퍼 자체에 대 한 포인터에 핸들을 전달 합니다. 공급자는 이 접근자를 사용하여 버퍼에 포함된 데이터를 전송할 방법을 확인합니다.  
  
4.  DBPARAMS 구조를 채웁니다. 입력 매개 변수에서 값이 읽히고 출력 매개 변수 값이 기록 되는 소비자 변수를 런타임에 전달 됩니다 **icommand:: Execute** DBPARAMS 구조에서입니다. DBPARAMS 구조에는 다음 3개의 요소가 포함됩니다.  
  
    -   접근자 핸들에 의해 지정된 바인딩에 따라 공급자가 입력 매개 변수 데이터를 가져오고 출력 매개 변수 데이터를 반환하는 버퍼에 대한 포인터  
  
    -   버퍼에 있는 매개 변수 집합의 수  
  
    -   3단계에서 만든 접근자 핸들  
  
5.  명령을 사용 하 여 실행 **icommand:: Execute**합니다.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>저장 프로시저 호출 방법  
 저장된 프로시저를 실행할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 OLE DB driver for SQL Server에서:  
  
-   ODBC CALL 이스케이프 시퀀스  
  
-   RPC(원격 프로시저 호출) 이스케이프 시퀀스  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 문  
  
### <a name="odbc-call-escape-sequence"></a>ODBC CALL 이스케이프 시퀀스  
 매개 변수 정보를 알고 있는 경우 호출 **icommandwithparameters:: Setparameterinfo** 메서드를 공급자에 매개 변수를 설명 합니다. 그렇지 않은 경우 저장 프로시저 호출에 ODBC CALL 구문을 사용하면 공급자는 도우미 함수를 호출하여 저장 프로시저 매개 변수 정보를 찾습니다.  
  
 매개 변수 정보(매개 변수 메타데이터)가 확실하지 않을 경우에는 ODBC CALL 구문을 사용하는 것이 좋습니다.  
  
 ODBC CALL 이스케이프 시퀀스를 사용한 프로시저 호출의 일반적인 구문은 다음과 같습니다.  
  
 {[**?=**]**call***procedure_name*[**(**[*parameter*][**,**[*parameter*]]...**)**]}  
  
 예를 들어:  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>RPC 이스케이프 시퀀스  
 RPC 이스케이프 시퀀스는 ODBC CALL의 저장 프로시저 호출 구문과 비슷합니다. 프로시저를 여러 번 호출한다면 저장 프로시저를 호출하는 3가지 방법 중 RPC 이스케이프 시퀀스가 가장 높은 성능을 제공합니다.  
  
 RPC 이스케이프 시퀀스를 사용하여 저장 프로시저를 실행할 경우 공급자는 ODBC CALL 구문에서와는 달리 매개 변수 정보를 확인하기 위한 어떠한 도우미 함수도 호출하지 않습니다. RPC 구문은 ODBC CALL 구문보다 간단하므로 명령이 구문 분석되는 시간이 더 빠르고 성능이 향상됩니다. 실행 하 여 매개 변수 정보를 제공 해야 하는 경우에 **icommandwithparameters:: Setparameterinfo**합니다.  
  
 RPC 이스케이프 시퀀스에서는 반환 값이 있어야 합니다. 저장 프로시저가 값을 반환하지 않으면 서버는 기본적으로 0을 반환합니다. 또한 저장 프로시저에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서를 열 수 없습니다. 저장된 프로시저는 암시적으로 준비에 대 한 호출은 **icommandprepare:: Prepare** 실패 합니다. 열 메타 데이터를 쿼리하지 수 RPC 호출을 준비 하려면 없기 때문에 Icolumnsinfo:: Getcolumninfo 및 icolumnsrowset:: Getcolumnsrowset DB_E_NOTPREPARED를 반환 합니다.  
  
 모든 매개 변수 메타데이터를 알고 있다면 RPC 이스케이프 시퀀스를 사용하여 저장 프로시저를 실행하는 것이 좋습니다.  
  
 다음은 RPC 이스케이프 시퀀스를 사용한 저장 프로시저 호출의 예입니다.  
  
```  
{rpc SalesByCategory}  
```  
  
 RPC 이스케이프 시퀀스를 보여 주는 샘플 응용 프로그램을 참조 하세요. [저장 프로시저 & #40; 실행 RPC 구문 & #41;를 사용 하 여 처리 반환 코드 및 출력 매개 변수 사용 & #40; OLE db& #41; ](../../oledb/ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Transact-SQL EXECUTE 문  
 ODBC CALL 이스케이프 시퀀스와 RPC 이스케이프 시퀀스는 저장된 프로시저를 호출 하기 위한 기본 메서드 대신 [EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md) 문. OLE DB Driver for SQL Server의 RPC 메커니즘을 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 명령 처리를 최적화 합니다. 이 RPC 프로토콜은 서버에서 수행되는 매개 변수 처리와 문 구문 분석의 대부분을 제거하여 성능을 향상시킵니다.  
  
 이의 예는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE** 문:  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>참고 항목  
 [저장된 프로시저](../../oledb/ole-db/stored-procedures.md)  
  
  
