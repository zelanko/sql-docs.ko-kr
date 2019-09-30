---
title: 변경 캡처를 위해 선택된 테이블 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ee52054e14c641aad64eaa96b146af86e048d95
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298701"
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>변경 캡처를 위해 선택된 테이블 변경

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 대화 상자에서 변경을 캡처할 선택된 테이블의 특정 열을 선택할 수 있습니다. 또한 **보안 역할** 및 **캡처 인스턴스** 정보를 편집할 수 있습니다.  
  
 이 대화 상자에서 변경을 캡처하도록 선택한 테이블을 다음과 같이 변경할 수 있습니다.  
  
 **CDC 인스턴스에 포함되는 열 변경:**  
  
 다음 중 하나 또는 모두를 수행합니다.  
  
-   포함할 추가 열의 옆에 있는 확인란을 선택합니다.  
  
-   더 이상 포함하지 않을 열의 옆에 있는 확인란을 선택 취소합니다.  
  
 **특정 열의 데이터 형식 변경**:  
  
 특정 열에 대해 다른 데이터 형식을 선택할 수 있습니다. 원본 데이터 형식과 호환되는 데이터 형식으로만 변경할 수 있습니다.  
  
 데이터 형식을 변경하려면 **데이터 형식** 열을 클릭하고 다른 데이터 형식을 선택합니다. 원본 데이터 형식과 호환되는 데이터 형식만 사용할 수 있습니다.  
  
> [!NOTE]  
>  추가 데이터 형식을 선택할 수 없는 경우 드롭다운 목록이 제공되지 않습니다.  
  
 **보안 역할 변경**  
  
 **보안 역할** 필드에서 새 이름을 입력하거나 보안 제어 역할의 이름을 편집합니다.  
  
 **캡처 인스턴스 변경 또는 추가**  
  
 **캡처 인스턴스** 필드에 캡처 인스턴스의 이름을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle 테이블 및 열 선택](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
