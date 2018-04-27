---
title: 차원 테이블 및 키 선택(느린 변경 차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3cc2148bf7433e185aa08c97317bc4d4e98be679
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>차원 테이블 및 키 선택(느린 변경 차원 마법사)
  **차원 테이블 및 키 선택** 페이지를 사용하여 로드할 차원 테이블을 선택할 수 있습니다. 데이터 흐름의 열을 로드하는 열에 매핑합니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **Connection manager**  
 목록에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 OLE DB 연결 관리자를 만듭니다.  
  
> [!NOTE]  
>  느린 변경 차원 마법사에서는 OLE DB 연결 관리자만 지원하며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 연결만 지원합니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 기존 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 OLE DB 연결을 만들 수 있습니다.  
  
 **테이블 또는 뷰**  
 목록에서 테이블이나 뷰를 선택합니다.  
  
 **입력 열**  
 입력 열 목록에서 매핑을 지정할 입력 열을 선택합니다.  
  
 **차원 열**  
 사용 가능한 차원 열을 모두 보여 줍니다.  
  
 **키 유형**  
 차원 열 중 하나를 비즈니스 키로 선택합니다. 비즈니스 키는 반드시 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [느린 변경 차원 마법사를 사용하여 출력 구성](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
