---
title: 클릭 광고 보고서 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 20c212e7829a04e1c6261a8818cebf7534d2529a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244353"
---
# <a name="clickthrough-reports-page-report-manager"></a>클릭 광고 보고서 페이지(보고서 관리자)
  클릭 광고 보고서는 보고서 내에 포함된 대화형 데이터를 클릭하면 관련된 데이터로 작성된 표를 표시합니다. 이러한 보고서는 보고서를 작성할 때 사용한 모델 내에 포함된 정보를 바탕으로 생성됩니다. 보고서 서버가 생성하는 클릭 광고 보고서를 사용하지 않으려면 사용자 지정 보고서를 만들어 보고서 서버에 게시하고 모델에 정의된 대화형 데이터 지점에 매핑하면 됩니다. 사용자 지정 보고서는 보고서 작성기에서 같은 모델을 통해 만든 다음 보고서 서버에 게시해야 합니다. 사용자 지정 보고서를 모델의 항목에 매핑하려면 보고서 관리자의 클릭 광고 보고서 페이지를 사용합니다.  
  
 클릭 광고 보고서 페이지는 미리 정의되고 게시된 보고서 작성기 보고서를 모델 내 특정 엔터티에 매핑할 수 있는 방법을 제공합니다. 보고서를 모델 내의 항목에 매핑하는 경우 해당 항목을 탐색하는 사용자는 보고서 서버에 의해 생성된 임시 보고서 대신 사용자 지정 보고서를 받게 됩니다.  
  
 사용자 지정 보고서를 제공하는 경우 보고서의 단일 인스턴스 버전과 여러 인스턴스 버전을 모두 포함해야 합니다. 사용자가 특정 엔터티를 탐색하는 데이터 경로에 따라 런타임에 사용자에게 단일 인스턴스 보고서가 제공되는지, 아니면 다중 인스턴스 보고서가 제공되는지가 결정됩니다. 어떤 버전의 보고서가 필요한지 항상 미리 알 수는 없습니다.  
  
 엔터티에 매핑하는 사용자 지정 보고서는 보고서 서버 폴더 계층을 통해 보안이 설정됩니다. 모델 항목을 보고서에 매핑하는 경우 해당 보고서를 탐색하는 사용자가 보고서를 사용할 수 없으면 사용자는 해당 사용자 지정 보고서 대신 보고서 서버에 의해 생성된 임시 보고서를 받게 됩니다.  
  
 액세스 권한이 있는 모든 보고서를 선택할 수 있지만 구성하는 모델용으로 만든 보고서만 선택하는 것이 좋습니다.  
  
> [!NOTE]  
>  클릭 광고 보고서의 모든 버전에서 사용할 수 없는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다. 조직에서 실행 중인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 잘 모를 경우 데이터베이스 관리자에게 문의하십시오.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>클릭 광고 보고서 페이지를 열려면  
  
1.  보고서 관리자를 열고 클릭 광고 보고서를 모델의 엔터티에 매핑할 모델을 찾습니다.  
  
2.  모델 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 모델의 **일반** 속성 페이지가 열립니다.  
  
4.  **클릭 광고** 탭을 선택합니다.  
  
## <a name="options"></a>변수  
 **모델 항목 계층**  
 사용자 지정 보고서를 제공할 수 있는 모델 네임스페이스의 엔터티, 폴더 및 항목을 표시합니다.  
  
 **단일 인스턴스 보고서**  
 사용자 탐색에 단일 인스턴스 데이터 뷰가 필요한 경우 사용할 사용자 지정 보고서를 지정합니다. 찾아보기 단추를 클릭하여 사용할 보고서를 선택할 수 있습니다.  
  
 **여러 인스턴스 보고서**  
 사용자 탐색에 여러 인스턴스 데이터 뷰가 필요한 경우 사용할 사용자 지정 보고서를 지정합니다. 찾아보기 단추를 클릭하여 사용할 보고서를 선택할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 게시](../../2014/reporting-services/publish-reports.md)  
  
  
