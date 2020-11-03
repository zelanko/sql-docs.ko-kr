---
description: catalog.remove_data_tap
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca55276a6108cd53ffae82fd4c40089023da20fb
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243622"
---
# <a name="catalogremove_data_tap"></a>catalog.remove_data_tap 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  실행 중인 구성 요소 출력에서 데이터 탭을 제거합니다. 데이터 탭의 고유 식별자는 실행 인스턴스와 연결되어 있습니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>인수  
 [ @data_tap_id = ] *data_tap_id*  
 catalog.add_data_tap 저장 프로시저를 사용하여 만든 데이터 탭의 고유 식별자입니다. *data_tap_id* 는 **bigint** 입니다.  
  
## <a name="remarks"></a>설명  

- 패키지에 이름이 같은 데이터 흐름 태스크가 두 개 이상 포함되어 있는 경우 주어진 이름을 가진 첫 번째 데이터 흐름 태스크에 데이터 탭이 추가됩니다.  
  
- 데이터 탭을 제거하려면 실행 인스턴스가 생성됨 상태여야 합니다( [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 보기의 **status** 열 값이 1).  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   사용자에게 MODIFY 권한이 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
