---
title: '태스크 12: 지식 (검색 기술 자료 검색) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d38af78e59a88e05fe874e4b4748b1f6f8b5049c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167703"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>태스크 12: 지식 검색(기술 자료 검색)
  수행한이 태스크에서는 합니다 **기술 자료 검색** 활동을 **Supplier ID** 하 고 **Supplier Name** 도메인. 이 시나리오에서 기술 자료 검색 프로세스는 주로 이러한 두 도메인의 값을 가져옵니다.  
  
 이 자습서에서는 기술 자료 구축을 처음부터 새로 시작했습니다. 기술 자료 검색 작업을 수행하여 기술 자료 만들기를 시작할 수도 있습니다. 클릭 하면 **기술 자료를 만듭니다** 기본 페이지에서 DQS 클라이언트 안내 하는 페이지로 **도메인 관리** 작업에 대해 선택한 작업입니다. 변경할 수 있습니다 합니다 **활동** 하 **기술 자료 검색** 후 다음 페이지에서 만들 수 있습니다 도메인 기술 자료 검색 프로세스의 일부로. 참조 [Perform Knowledge Discovery](http://msdn.microsoft.com/library/hh510398.aspx) 대 한 자세한 내용은 합니다.  
  
1.  DQS 클라이언트의 기본 페이지에서에 **최근 기술 자료** 섹션에서 **오른쪽 화살표** 옆에 **공급 업체** 기술 자료 및 클릭 **기술 검색**합니다. 을 클릭할 수 있습니다 **기술 자료 열기**를 선택 **공급 업체** 에서 합니다 **기술 자료 목록이**선택, **기술 자료 검색**으로 **활동** 을 클릭 **다음**합니다.  
  
     ![Main에서 기술 자료 검색 메뉴 페이지](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Main에서 기술 자료 검색 메뉴 페이지")  
  
2.  선택 **Excel 파일로** 에 대 한 **데이터 원본**합니다.  
  
3.  클릭 **찾아보기**이동 하 고 선택 **Suppliers.xls**를 클릭 하 고 **열기**합니다.  
  
4.  선택 **Suppliers for Discovery** 에 대 한 **워크시트**합니다.  
  
5.  에 **매핑을** 섹션에서 **SupplierID** 에서 열을 **Excel** 파일을 **Supplier ID** 도메인 및  **Supplier Name** 열을 **Supplier Name** 사용 하 여 도메인 **드롭 다운 목록을**합니다. Excel 파일에 대 한 샘플 데이터에는 **Supplier ID** 하 고 **Supplier Name** 도메인입니다. 검색 프로세스에서 값을 검색하려는 도메인을 선택할 수 있습니다. 이 페이지에서 도메인을 만들고 원본 열을 이러한 도메인에 매핑할 수 있습니다. 도메인 관리 작업 중에 도메인을 만들지 않고 기술 자료 검색 작업 중에 도메인을 만드는 것은 드문 일이 아닙니다.  
  
     ![검색 프로세스의 맵 페이지](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "검색 프로세스의 맵 페이지")  
  
6.  클릭 **다음** 으로 전환 합니다 **Discover** 페이지입니다.  
  
7.  에 **검색** 페이지에서 클릭 **시작** 검색 프로세스를 시작 합니다. 열에서 검색이 수행 됩니다 **SupplierID** 하 고 **Supplier Name** 에 **Suppliers.xls** 파일입니다. 합니다 **Supplier ID** 하 고 **Supplier Name** 도메인 검색 으로부터 가져온 지식이으로 채워져야 합니다.  
  
     ![검색 프로세스의 검색 페이지](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "검색 프로세스의 검색 페이지")  
  
8.  분석이 완료 되 면 검토 합니다 **원본 통계** 에 **Profiler 탭** 페이지의 맨 아래에서. 사용 하 여 10 개의 새 레코드 총 20 개의 값을 표시 (**SupplierID** 및 **Supplier Name** 에서 값을 **Excel 워크시트**) 검색 되었습니다. 또한 새 값, 고유 값, 새로운 고유 값 및 올바른 값의 개수도 확인할 수 있습니다. 오른쪽 목록 상자에서는 검색 프로세스에 포함된 각 도메인에 대해 보다 자세한 정보를 확인할 수 있습니다. Completeness 열에서 상태 표시줄 위로 마우스를 가져가면 원본의 열에 누락된 값이 있는지 확인할 수 있습니다.  
  
     ![기술 자료 검색 결과](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "기술 자료 검색 결과")  
  
9. 클릭 **다음** 으로 전환 합니다 **도메인 값 관리** 페이지입니다.  
  
10. 에 **도메인 값 관리** 페이지에서 클릭 **Supplier Name** 도메인 목록에서 도메인입니다.  
  
11. 오른쪽 창에서 마우스 오른쪽 단추로 클릭 **Lazy Country Storex** (이때 'x' 끝)를 선택 하 고 **Lazy Country Store**합니다. DQS는 도메인에서 맞춤법 검사기를 실행한 후 이 변경을 제안합니다. 기본적으로 도메인을 만들면 맞춤법 검사기가 사용하도록 설정됩니다.  
  
     ![올바른 공급자 이름-Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "올바른 공급자 이름-Lazy Country Store")  
  
12. 도메인 값 목록에 있는지를 확인 값 **Lazy Country Storex** 오류로 설정 됩니다 (빨간색 **X** 표시) 사용 하 여 **Lazy Country Store** 수정 및 합니다 **Lazy Country Store** 유효한 값으로도 추가 됩니다.  
  
     ![도메인 값 및 값 수정](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "도메인 값 및 값 수정")  
  
13. **마침**을 클릭합니다.  
  
14. 온 **SQL Server Data Quality Services** 대화 상자, 클릭 **게시**합니다.  
  
15. 클릭 **확인** 성공 메시지 상자에서.  
  
     이 자습서의 첫 번째 단원이 완료되었습니다.  
  
## <a name="next-step"></a>다음 단계  
 [2단원: 공급자 기술 자료를 사용하여 공급자 데이터 정리](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
