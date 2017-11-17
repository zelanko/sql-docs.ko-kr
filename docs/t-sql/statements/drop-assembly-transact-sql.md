---
title: DROP ASSEMBLY (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c38654a3ce90b4e1605cfdbe1db7a49ddac8b6b1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 어셈블리 및 모든 관련 파일을 제거합니다. 어셈블리를 사용 하 여 만들어진 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) 를 사용 하 여 수정할 [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 어셈블리를 삭제 합니다.  
  
 *assembly_name*  
 삭제할 어셈블리의 이름입니다.  
  
 WITH NO DEPENDENTS  
 를 지정 하는 경우만 삭제 *assembly_name* 및 어셈블리에 의해 참조 되는 종속 어셈블리의 없음. 지정 하지 않으면 DROP ASSEMBLY 떨어지면 *assembly_name* 과 모든 종속 어셈블리입니다.  
  
## <a name="remarks"></a>주의  
 어셈블리를 삭제하면 데이터베이스에서 어셈블리와 원본 코드 및 디버그 파일 등의 모든 관련 파일이 제거됩니다.  
  
 NO DEPENDENTS를 지정 하지 않으면 DROP ASSEMBLY 떨어지면 *assembly_name* 과 모든 종속 어셈블리입니다. 종속 어셈블리를 삭제하려는 시도가 실패하면 DROP ASSEMBLY가 오류를 반환합니다.  
  
 어셈블리가 데이터베이스에 있는 다른 어셈블리에서 참조되거나 현재 데이터베이스의 CLR(공용 언어 런타임) 함수, 프로시저, 트리거, 사용자 정의 형식 또는 집계에서 사용되면 DROP ASSEMBLY가 오류를 반환합니다.  
  
 DROP ASSEMBLY는 현재 실행되고 있는 어셈블리를 참조하는 코드를 방해하지 않습니다. 그러나 DROP ASSEMBLY를 실행한 후에는 어셈블리 코드를 호출하려는 모든 시도가 실패합니다.  
  
## <a name="permissions"></a>Permissions  
 어셈블리 소유권이나 어셈블리에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HelloWorld` 어셈블리가 이미 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 생성된 것으로 가정합니다.  
  
```  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [어셈블리 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER assembly&#40; Transact SQL &#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [어셈블리에 대 한 정보 가져오기](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  

