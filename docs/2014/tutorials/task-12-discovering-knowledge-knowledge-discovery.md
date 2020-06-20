---
title: '작업 12: 기술 자료 검색 (기술 자료 검색) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0bad2760a5dc9b16b24d75bb35617759543205f3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064775"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>태스크 12: 지식 검색(기술 자료 검색)
  이 작업에서는 **공급자 ID** 및 **공급자 이름** 도메인에 대 한 **기술 자료 검색** 작업을 수행 합니다. 이 시나리오에서 기술 자료 검색 프로세스는 주로 이러한 두 도메인의 값을 가져옵니다.  
  
 이 자습서에서는 기술 자료 구축을 처음부터 새로 시작했습니다. 기술 자료 검색 작업을 수행하여 기술 자료 만들기를 시작할 수도 있습니다. 기본 페이지에서 **기술 자료 만들기** 를 클릭 하면 DQS 클라이언트에서 작업에 대해 선택한 **도메인 관리** 작업이 있는 페이지로 이동 합니다. **활동** 을 **기술 자료 검색** 으로 변경 하 고 다음 페이지에서 기술 자료 검색 프로세스의 일부로 도메인을 만들 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](https://msdn.microsoft.com/library/hh510398.aspx) 을 참조 하세요.  
  
1.  DQS 클라이언트의 기본 페이지에 있는 **최근 기술** 자료 섹션에서 **Suppliers** 기술 자료 옆에 있는 **오른쪽 화살표** 를 클릭 하 고 **기술 자료 검색**을 클릭 합니다. 또는 기술 자료 **열기**를 클릭 하 고 **기술 자료 목록**에서 **Suppliers** 를 선택한 후 **기술 자료 검색** 을 **작업** 으로 선택 하 고 **다음**을 클릭 합니다.  
  
     ![주 페이지의 기술 자료 검색 메뉴](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "주 페이지의 기술 자료 검색 메뉴")  
  
2.  **데이터 원본**에 대해 **Excel 파일** 을 선택 합니다.  
  
3.  **찾아보기**를 클릭 하 고 **Suppliers.xls**찾아서 선택한 다음 **열기**를 클릭 합니다.  
  
4.  검색할 **공급자를** **워크시트**에 대해 선택 합니다.  
  
5.  **매핑** 섹션에서 **드롭다운 목록을**사용 하 여 **Excel** 파일 **의 공급 업체 열을** 공급자 **ID** 도메인 **및 공급자 이름 열** 에 **Supplier Name** 매핑합니다. Excel 파일에는 **공급자 ID** 및 **공급자 이름** 도메인에 대 한 샘플 데이터가 있습니다. 검색 프로세스에서 값을 검색하려는 도메인을 선택할 수 있습니다. 이 페이지에서 도메인을 만들고 원본 열을 이러한 도메인에 매핑할 수 있습니다. 도메인 관리 작업 중에 도메인을 만들지 않고 기술 자료 검색 작업 중에 도메인을 만드는 것은 드문 일이 아닙니다.  
  
     ![검색 프로세스의 맵 페이지](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "검색 프로세스의 맵 페이지")  
  
6.  **다음** 을 클릭 하 여 **검색** 페이지로 전환 합니다.  
  
7.  **검색 페이지에서** **시작** 을 클릭 하 여 검색 프로세스를 시작 합니다. 검색은 **Suppliers.xls** 파일의 공급자 **SupplierID** 이름 및 **공급자 이름** 열에 대해 수행 됩니다. **공급자 ID** 및 **공급자 이름** 도메인은 검색에서 가져온 정보로 채워야 합니다.  
  
     ![검색 프로세스의 검색 페이지](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "검색 프로세스의 검색 페이지")  
  
8.  분석이 완료 되 면 페이지 아래쪽의 **프로파일러 탭** 에서 **원본 통계** 를 검토 합니다. 총 20 개의 값 (**공급** 업체 및 **Excel 워크시트**의 **공급자 이름** 값)이 포함 된 10 개의 새 레코드가 검색 되었습니다. 또한 새 값, 고유 값, 새로운 고유 값 및 올바른 값의 개수도 확인할 수 있습니다. 오른쪽 목록 상자에서는 검색 프로세스에 포함된 각 도메인에 대해 보다 자세한 정보를 확인할 수 있습니다. Completeness 열에서 상태 표시줄 위로 마우스를 가져가면 원본의 열에 누락된 값이 있는지 확인할 수 있습니다.  
  
     ![기술 자료 검색 결과](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "기술 자료 검색 결과")  
  
9. **다음** 을 클릭 하 여 **도메인 값 관리** 페이지로 전환 합니다.  
  
10. **도메인 값 관리** 페이지의 도메인 목록에서 **공급자 이름** 도메인을 클릭 합니다.  
  
11. 오른쪽 창에서 **Lazy Country Storex** (끝에 ' x ' 표시)를 마우스 오른쪽 단추로 클릭 하 고 **lazy country Store**를 선택 합니다. DQS는 도메인에서 맞춤법 검사기를 실행한 후 이 변경을 제안합니다. 기본적으로 도메인을 만들면 맞춤법 검사기가 사용하도록 설정됩니다.  
  
     ![올바른 공급자 이름 - Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "올바른 공급자 이름 - Lazy Country Store")  
  
12. 도메인 값 목록에서 **Lazy Country Storex** 값이 수정으로 **lazy country store** 를 사용 하 여 오류 (빨간색 **X** 표시)로 설정 되어 있는지 확인 하 고 **lazy country store** 도 유효한 값으로 추가 합니다.  
  
     ![도메인 값 및 다음으로 수정 값](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "도메인 값 및 다음으로 수정 값")  
  
13. **Finish**를 클릭합니다.  
  
14. **SQL Server Data Quality Services** 대화 상자에서 **게시**를 클릭 합니다.  
  
15. 성공 메시지 상자에서 **확인을** 클릭 합니다.  
  
     이 자습서의 첫 번째 단원이 완료되었습니다.  
  
## <a name="next-step"></a>다음 단계  
 [2단원: 공급자 기술 자료를 사용하여 공급자 데이터 정리](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
