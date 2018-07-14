---
title: 데이터베이스 게시(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fc01e05624d55b2f8bfda2c7d747d03604f17fac
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260909"
---
# <a name="publish-a-database-sql-server-management-studio"></a>데이터베이스 게시(SQL Server Management Studio)
  **스크립트 생성 및 게시 마법사** 를 사용하여 전체 데이터베이스 또는 개별 데이터베이스 개체를 웹 호스팅 공급자에 게시할 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 기능은 데이터베이스 게시 마법사에서 제공했던 기능입니다. 게시 기능이 스크립트 생성 및 게시 마법사에 추가되었고 데이터베이스 게시 마법사는 더 이상 사용되지 않습니다.  
  
## <a name="generate-and-publish-scripts-wizard"></a>스크립트 생성 및 게시 마법사  
 스크립트 생성 및 게시 마법사를 사용하여 데이터베이스 또는 선택된 데이터베이스 개체를 웹 호스팅 공급자에 게시할 수 있습니다. SQL Server 웹 호스팅 공급자는 웹 서비스에 대한 연결 인터페이스입니다. 웹 서비스는 CodePlex의 SQL Server Hosting Toolkit에 있는 데이터베이스 게시 서비스 프로젝트를 사용하여 생성됩니다. 웹 서비스를 통해 웹 호스터 고객은 스크립트 생성 및 게시 마법사를 사용하여 데이터베이스를 서비스로 쉽게 게시할 수 있습니다. SQL Server Hosting Toolkit을 다운로드하는 방법은 [SQL Server 데이터 게시 서비스(SQL Server Database Publishing Services)](http://go.microsoft.com/fwlink/?LinkId=142025)를 참조하세요.  
  
 스크립트 생성 및 게시 마법사는 데이터베이스를 전송하기 위한 스크립트를 만드는 데 사용할 수도 있습니다.  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>웹 서비스에 데이터베이스를 게시하려면  
  
1.  개체 탐색기에서 **데이터베이스**를 확장하고 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음, **태스크**를 가리키고 **스크립트 생성 및 게시**를 클릭합니다. 마법사의 단계에 따라 게시할 데이터베이스 개체를 스크립팅합니다.  
  
2.  **개체 선택** 페이지에서 웹 호스팅 서비스에 게시할 개체를 선택합니다.  
  
3.  **스크립팅 옵션 설정** 페이지에서 **웹 서비스에 게시**를 선택합니다.  
  
    1.  **공급자** 상자에서 웹 서비스의 공급자를 지정합니다. 웹 호스팅 공급자를 구성하지 않은 경우 **공급자 관리** 를 선택하고 **공급자 관리** 대화 상자를 사용하여 웹 서비스의 공급자를 구성합니다.  
  
    2.  고급 게시 옵션을 지정하려면 **웹 서비스에 게시** 섹션에서 **고급** 단추를 선택합니다.  
  
4.  **요약** 페이지에서 선택 항목을 검토합니다. 선택 항목을 변경하려면 **이전** 을 클릭합니다. 선택한 개체를 게시하려면 **다음** 을 클릭합니다.  
  
5.  **스크립트 저장 또는 게시** 페이지에서 게시 진행률을 모니터링합니다.  
  
## <a name="see-also"></a>관련 항목  
 [스크립트 생성&#40;SQL Server Management Studio&#41;](../scripting/generate-scripts-sql-server-management-studio.md)   
 [데이터베이스를 다른 서버로 복사](copy-databases-to-other-servers.md)  
  
  
