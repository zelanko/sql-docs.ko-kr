---
title: MDS 저장소에 연결
description: Excel용 Master Data Services 추가 기능에서 데이터를 로드 하거나 게시 하려면 먼저 MDS(Master Data Services) 리포지토리에 연결 해야 합니다.
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cc8148f2e24c7007c75309da407a188ec6c908ca
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "92257710"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>MDS 저장소에 연결(Excel용 MDS 추가 기능)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서는 데이터를 로드하거나 게시하기 전에 MDS 리포지토리에 연결해야 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
### <a name="to-connect-to-an-mds-repository"></a>MDS 저장소에 연결하려면  
  
1.  MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]의 **마스터 데이터** 탭에 있는 **연결 및 로드** 그룹에서 **연결** 단추 아래의 화살표를 클릭하고 **연결 관리**를 클릭합니다.  
  
2.  **연결 관리** 대화 상자의 **새 연결** 섹션에서 **새 연결 만들기**를 클릭합니다.  
  
3.  **새로 만들기**를 클릭합니다.  
  
4.  **새 연결 추가** 대화 상자의 **설명** 필드에서 연결에 대한 설명을 입력합니다. 이 연결은 사용자가 도구 모음에서 **연결** 단추 아래의 화살표를 클릭할 때 표시됩니다.  
  
5.  **MDS 서버 주소** 상자에 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션의 URL(예: `https://contoso/mds`)을 입력합니다.  
  
    > [!NOTE]  
    >  컴퓨터 이름을 사용해야 합니다. "localhost"는 사용하지 마십시오.  
  
6.  **확인**을 클릭합니다. 이 이름은 **기존 연결** 섹션에 표시됩니다.  
  
7.  선택적으로 **테스트** 를 클릭하여 연결을 테스트합니다. 확인 또는 오류 대화 상자가 표시됩니다. **확인** 을 클릭하여 닫습니다.  
  
8.  **연결**을 클릭합니다. **Master Data Services** 창이 표시됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)  
  
-   [내보내기 전 데이터 필터링&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>참고 항목  
 [연결&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
  
