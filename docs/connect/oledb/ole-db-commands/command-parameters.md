---
title: 명령 매개 변수 | Microsoft Docs
description: 명령 매개 변수
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
manager: craigg
ms.openlocfilehash: 9b4e12d36c00769be83e01e47fafbd2e18421aa1
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106429"
---
# <a name="command-parameters"></a>명령 매개 변수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  매개 변수는 명령 텍스트에서 물음표(?) 문자로 표시됩니다. 예를 들어 다음 SQL 문은 한 개의 입력 매개 변수를 표시합니다.  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 네트워크 트래픽을 줄여 성능을 향상하기 위해 SQL Server용 OLE DB 드라이버는 명령 실행 전에 **ICommandWithParameters::GetParameterInfo** 또는 **ICommandPrepare::Prepare**를 호출하지 않는 한 매개 변수 정보를 자동으로 파생시키지 않습니다. 이 OLE DB Driver for SQL Server를 자동으로 나타나지 않을 것을 의미 합니다.  
  
-   **ICommandWithParameters::SetParameterInfo**에 지정된 데이터 형식이 올바른지 확인합니다.  
  
-   접근자 바인딩 정보에 지정된 DBTYPE에서 매개 변수의 올바른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식으로 매핑  
  
 응용 프로그램에서 매개 변수의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 호환되지 않는 데이터 형식을 지정하면 이러한 방법 중 하나에서 오류나 전체 자릿수 손실이 발생할 수 있습니다.  
  
 이 문제가 발생하지 않게 하려면 응용 프로그램에서 다음을 수행해야 합니다.  
  
-   **ICommandWithParameters::SetParameterInfo**를 하드 코딩할 경우 *pwszDataSourceType*이 매개 변수의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 일치하는지 확인합니다.  
  
-   접근자를 하드 코딩할 경우 매개 변수에 바인딩되는 DBTYPE 값이 매개 변수의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 같은 형식인지 확인합니다.  
  
-   공급자가 매개 변수의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 동적으로 얻을 수 있도록 **ICommandWithParameters::GetParameterInfo**를 호출하는 응용 프로그램을 코딩합니다. 이로 인해 서버로의 네트워크 왕복이 추가로 발생합니다.  
  
> [!NOTE]  
>  공급자에서는 FROM 절이 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UPDATE 또는 DELETE 문, 매개 변수를 포함하는 하위 쿼리에 종속된 SQL 문, 비교, like 또는 한정된 조건자의 두 식이나 매개 변수 중 하나가 함수의 매개 변수인 쿼리에 매개 변수 표식이 포함된 SQL 문에 대해 **ICommandWithParameters::GetParameterInfo**를 호출할 수 없습니다. 또한 SQL 문을 일괄 처리할 경우 공급자에서는 일괄 처리의 첫 번째 문 다음에 나오는 문의 매개 변수 표식에 대해 **ICommandWithParameters::GetParameterInfo**를 호출할 수 없습니다. 주석(/* \*/)이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령에 허용되지 않습니다.  
  
 OLE DB Driver for SQL Server는 SQL 문 명령에서 입력된 매개 변수를 지원합니다. 프로시저 호출 명령에는 OLE DB Driver for SQL Server는 입력, 출력 및 입/출력 매개 변수를 지원합니다. 실행 시(반환되는 행 집합이 없는 경우에만 해당) 또는 반환된 행 집합이 응용 프로그램에서 모두 사용된 경우에 출력 매개 변수 값이 응용 프로그램에 반환됩니다. 반환된 값이 유효한지 확인하려면 **IMultipleResults**를 사용하여 행 집합을 강제로 소비합니다.  
  
 저장 프로시저 매개 변수의 이름은 DBPARAMBINDINFO 구조에서 지정하지 않아도 됩니다. SQL Server용 OLE DB 드라이버가 매개 변수 이름을 무시하고 **ICommandWithParameters::SetParameterInfo**의 *rgParamOrdinals* 멤버에 지정된 서수만 사용하도록 *pwszName* 멤버 값에 NULL을 사용합니다. 명령 텍스트에 명명된 매개 변수와 명명되지 않은 매개 변수가 모두 포함된 경우 모든 명명되지 않은 매개 변수를 명명된 매개 변수보다 먼저 지정해야 합니다.  
  
 저장 프로시저 매개 변수의 이름을 지정하면 SQL Server용 OLE DB 드라이버는 이름이 유효한지 확인합니다. OLE DB Driver for SQL Server는 잘못 된 매개 변수 이름을 소비자 로부터 받을 때 오류를 반환 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 및 UDT(사용자 정의 형식)에 대한 지원을 제공하기 위해 SQL Server용 OLE DB 드라이버는 새로운 [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) 인터페이스를 구현합니다.  
  
## <a name="see-also"></a>참고 항목  
 [도구](../../oledb/ole-db-commands/commands.md)  
  
  
