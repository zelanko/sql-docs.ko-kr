---
title: 차원 테이블 및 키 선택(느린 변경 차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 403ce296913bfcfbf55aedb75e989dd5d296c6c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725889"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>차원 테이블 및 키 선택(느린 변경 차원 마법사)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **차원 테이블 및 키 선택** 페이지를 사용하여 로드할 차원 테이블을 선택할 수 있습니다. 데이터 흐름의 열을 로드하는 열에 매핑합니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
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
  
  
