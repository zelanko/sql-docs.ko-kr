---
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f2c9b5d9333c201120e5f3a3e392c59012a8ac7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 중인 구성 요소 출력에서 데이터 탭을 제거합니다. 데이터 탭의 고유 식별자는 실행 인스턴스와 연결되어 있습니다.  
  
## <a name="syntax"></a>구문  
  
```tsql  
remove_data_tap [ @data_tap_id = ] data_tap_id  
  
```  
  
## <a name="arguments"></a>인수  
 [ @data_tap_id =] *data_tap_id*  
 catalog.add_data_tap 저장 프로시저를 사용하여 만든 데이터 탭의 고유 식별자입니다. *data_tap_id* 은 **bigint**합니다.  
  
## <a name="remarks"></a>주의  
 패키지에 이름이 같은 데이터 흐름 태스크가 두 개 이상 포함되어 있는 경우 주어진 이름을 가진 첫 번째 데이터 흐름 태스크에 데이터 탭이 추가됩니다.  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 탭 데이터를 제거 하려면을 실행 인스턴스가 생성 됨 상태 여야 합니다 (값 1에는 **상태** 의 열은 [catalog.operations &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)보기).  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   사용자에게 MODIFY 권한이 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
