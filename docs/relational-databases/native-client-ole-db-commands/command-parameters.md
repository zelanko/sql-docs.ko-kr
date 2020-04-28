---
title: 명령 매개 변수 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5db24ee3b68d1a8989200479a3ce4018e63a5177
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304522"
---
# <a name="command-parameters"></a>명령 매개 변수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  매개 변수는 명령 텍스트에서 물음표(?) 문자로 표시됩니다. 예를 들어 다음 SQL 문은 한 개의 입력 매개 변수를 표시합니다.  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 네트워크 트래픽을 줄여 성능을 향상 시키기 위해 명령을 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하기 전에 **ICommandWithParameters:: GetParameterInfo** 또는 **ICommandPrepare::P repare** 를 호출 하지 않으면 Native Client OLE DB 공급자가 자동으로 매개 변수 정보를 파생 시 키 지 않습니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음을 자동으로 수행 하지 않습니다.  
  
-   **ICommandWithParameters::SetParameterInfo**에 지정된 데이터 형식이 올바른지 확인합니다.  
  
-   접근자 바인딩 정보에 지정된 DBTYPE에서 매개 변수의 올바른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 매핑  
  
 애플리케이션에서 매개 변수의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 호환되지 않는 데이터 형식을 지정하면 이러한 방법 중 하나에서 오류나 전체 자릿수 손실이 발생할 수 있습니다.  
  
 이 문제가 발생하지 않게 하려면 애플리케이션에서 다음을 수행해야 합니다.  
  
-   **ICommandWithParameters::SetParameterInfo**를 하드 코딩할 경우 *pwszDataSourceType*이 매개 변수의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 일치하는지 확인합니다.  
  
-   접근자를 하드 코딩할 경우 매개 변수에 바인딩되는 DBTYPE 값이 매개 변수의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 같은 형식인지 확인합니다.  
  
-   공급자가 매개 변수의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 동적으로 얻을 수 있도록 **ICommandWithParameters::GetParameterInfo**를 호출하는 애플리케이션을 코딩합니다. 이로 인해 서버로의 네트워크 왕복이 추가로 발생합니다.  
  
> [!NOTE]  
>  공급자에서는 FROM 절이 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UPDATE 또는 DELETE 문, 매개 변수를 포함하는 하위 쿼리에 종속된 SQL 문, 비교, like 또는 한정된 조건자의 두 식이나 매개 변수 중 하나가 함수의 매개 변수인 쿼리에 매개 변수 표식이 포함된 SQL 문에 대해 **ICommandWithParameters::GetParameterInfo**를 호출할 수 없습니다. 또한 SQL 문을 일괄 처리할 경우 공급자에서는 일괄 처리의 첫 번째 문 다음에 나오는 문의 매개 변수 표식에 대해 **ICommandWithParameters::GetParameterInfo**를 호출할 수 없습니다. 주석(/* \*/)이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령에 허용되지 않습니다.  
  
 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 SQL 문 명령에서 입력 매개 변수를 지원 합니다. 프로시저 호출 명령에서 Native Client OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자는 입력, 출력 및 입/출력 매개 변수를 지원 합니다. 실행 시(반환되는 행 집합이 없는 경우에만 해당) 또는 반환된 행 집합이 애플리케이션에서 모두 사용된 경우에 출력 매개 변수 값이 애플리케이션에 반환됩니다. 반환된 값이 유효한지 확인하려면 **IMultipleResults**를 사용하여 행 집합을 강제로 소비합니다.  
  
 저장 프로시저 매개 변수의 이름은 DBPARAMBINDINFO 구조에서 지정하지 않아도 됩니다. *PwszName* 멤버의 값에 NULL을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 매개 변수 이름을 무시 하 고 **ICommandWithParameters:: SetParameterInfo**의 *rgParamOrdinals* 멤버에 지정 된 서 수만 사용 하도록 지정 합니다. 명령 텍스트에 명명된 매개 변수와 명명되지 않은 매개 변수가 모두 포함된 경우 모든 명명되지 않은 매개 변수를 명명된 매개 변수보다 먼저 지정해야 합니다.  
  
 저장 프로시저 매개 변수의 이름이 지정 된 경우 Native Client OLE DB 공급자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 이름을 확인 하 여 유효한 지 확인 합니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 소비자 로부터 잘못 된 매개 변수 이름을 받을 때 오류를 반환 합니다.  
  
> [!NOTE]  
>  XML 및 UDT ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 정의 형식)에 대 한 지원을 노출 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 새 [ISSCommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) 인터페이스를 구현 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [명령](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
