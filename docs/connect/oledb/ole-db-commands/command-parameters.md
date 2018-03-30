---
title: 명령 매개 변수 | Microsoft Docs
description: 명령 매개 변수
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4d2802302b31943d0c8d7fcc53158b12ad04132
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="command-parameters"></a>명령 매개 변수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  매개 변수는 명령 텍스트에서 물음표(?) 문자로 표시됩니다. 예를 들어 다음 SQL 문은 한 개의 입력 매개 변수를 표시합니다.  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 네트워크 트래픽을 줄여 성능을 향상 시키려면는 OLE DB Driver for SQL Server 파생 되지 않은 자동으로 매개 변수 정보 하지 않는 한 **icommandwithparameters:: Getparameterinfo** 또는 **ICommandPrepare:: 준비** 명령을 실행 하기 전에 호출 됩니다. 이 OLE DB Driver for SQL Server를 자동으로 나타나지 않을 것을 의미 합니다.  
  
-   지정 된 데이터 형식이 올바른지 확인 **icommandwithparameters:: Setparameterinfo**합니다.  
  
-   접근자 바인딩 정보에 지정된 DBTYPE에서 매개 변수의 올바른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식으로 매핑  
  
 응용 프로그램에서 매개 변수의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 호환되지 않는 데이터 형식을 지정하면 이러한 방법 중 하나에서 오류나 전체 자릿수 손실이 발생할 수 있습니다.  
  
 이 문제가 발생하지 않게 하려면 응용 프로그램에서 다음을 수행해야 합니다.  
  
-   되도록 *pwszDataSourceType* 일치는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하드 코딩 하는 경우 데이터 형식 매개 변수에 대해 **icommandwithparameters:: Setparameterinfo**합니다.  
  
-   접근자를 하드 코딩할 경우 매개 변수에 바인딩되는 DBTYPE 값이 매개 변수의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 같은 형식인지 확인합니다.  
  
-   호출 하 여 응용 프로그램을 코딩할 **icommandwithparameters:: Getparameterinfo** 공급자 얻을 수 있도록는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 매개 변수의 데이터 형식을 동적으로 합니다. 이로 인해 서버로의 네트워크 왕복이 추가로 발생합니다.  
  
> [!NOTE]  
>  공급자 호출을 지원 하지 않습니다 **icommandwithparameters:: Getparameterinfo** 에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UPDATE 또는 DELETE 문의 FROM 절;이 포함 된 지정 매개 변수를 포함 하는 하위 쿼리에 SQL 문에 대 정량화 된 조건자; 또는 like, 비교의 두 식이나 매개 변수 표식이 포함 된 SQL 문에 대 한 또는 쿼리 함수에 매개 변수는 매개 변수 중 하나입니다. SQL 문의 일괄 처리를 처리할 때는 공급자도 지원 하지 않습니다 호출 **icommandwithparameters:: Getparameterinfo** 문 일괄 처리의 첫 번째 문 다음에 매개 변수 표식에 대 한 합니다. 주석 (/ * \*/)에서 허용 되지 않습니다는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령입니다.  
  
 OLE DB Driver for SQL Server는 SQL 문 명령에서 입력된 매개 변수를 지원합니다. 프로시저 호출 명령에는 OLE DB Driver for SQL Server 입력, 출력 및 입/출력 매개 변수를 지원합니다. 실행 시(반환되는 행 집합이 없는 경우에만 해당) 또는 반환된 행 집합이 응용 프로그램에서 모두 사용된 경우에 출력 매개 변수 값이 응용 프로그램에 반환됩니다. 반환 된 값이 유효한 지 하려면 사용 하 여 **IMultipleResults** 강제로 행 집합 소비 합니다.  
  
 저장 프로시저 매개 변수의 이름은 DBPARAMBINDINFO 구조에서 지정하지 않아도 됩니다. 값에 대해 NULL을 사용 하 여는 *pwszName* 표시 되는 OLE DB Driver for SQL Server 해야 무시 매개 변수 이름에 지정 된 서 수에만 사용 하 여 멤버는 *rgParamOrdinals* 의구성원 **Icommandwithparameters:: Setparameterinfo**합니다. 명령 텍스트에 명명된 매개 변수와 명명되지 않은 매개 변수가 모두 포함된 경우 모든 명명되지 않은 매개 변수를 명명된 매개 변수보다 먼저 지정해야 합니다.  
  
 저장된 프로시저 매개 변수의 이름을 지정 하는 경우에 OLE DB Driver for SQL Server 유효한 지 확인 하는 이름을 확인 합니다. OLE DB Driver for SQL Server 소비자 로부터 잘못 된 매개 변수 이름의 받을 때 오류가 반환 됩니다.  
  
> [!NOTE]  
>  에 대 한 지원을 공개 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 및 사용자 정의 형식 (UDT)는 OLE DB Driver for SQL Server를 구현 하는 새 [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) 인터페이스입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [도구](../../oledb/ole-db-commands/commands.md)  
  
  
