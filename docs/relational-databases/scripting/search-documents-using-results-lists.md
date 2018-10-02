---
title: 결과 목록을 사용하여 문서 검색 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], result lists
- result list searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], multiple files
- Query Editor [SQL Server Management Studio], search multiple files
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ec4a2194ed8532788ac9bcb96ab1839bb352701
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814971"
---
# <a name="search-documents-using-results-lists"></a>결과 목록을 사용하여 문서 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **찾기 및 바꾸기** 대화 상자를 사용하면 프로젝트나 솔루션 또는 파일 시스템 폴더의 모든 파일을 검색하여 바꿀 수 있으며 이러한 파일이 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 열려 있지 않은 경우에도 마찬가지입니다. **찾기 및 바꾸기** 대화 상자에서 수행한 검색 조건과 일치하는 항목이 찾기 결과 1 및 찾기 결과 2 창에 나타나며 일치하는 항목이 포함된 줄에서 해당 텍스트를 볼 수 있습니다.  
  
### <a name="to-search-in-multiple-files"></a>여러 파일을 검색하려면  
  
1.  **편집** 메뉴에서 **찾기 및 바꾸기** 를 가리킨 다음 **파일에서 찾기**를 클릭합니다.  
  
2.  **찾을 내용** 입력란에 검색할 텍스트를 입력합니다.  
  
3.  **찾는 위치** 목록에서 **모든 열린 문서**, **현재 프로젝트**또는 **전체 솔루션**을 클릭하거나 디렉터리 경로를 입력합니다.  
  
4.  **파일 형식** 목록에서 나열된 파일 확장명 집합 중 하나를 선택하거나 검색할 파일 형식에 대한 확장명을 쉼표로 구분하여 입력합니다. 대신 \*에서 열려 있지 않은 경우에도 마찬가지입니다.\* 를 사용하여 **찾는 위치** 드롭다운 목록에 나열된 디렉터리에서 모든 파일을 검색할 수 있습니다.  
  
5.  검색의 정확도를 높이려면 나머지 검색 옵션 중에서 원하는 옵션을 선택합니다.  
  
6.  **찾기** 를 클릭하여 검색을 시작합니다.  
  
 검색 조건과 일치하는 항목이 기본적으로 찾기 결과 1 창에 표시됩니다. 찾기 결과 1 창에서 각 항목을 두 번 클릭하여 검색 조건과 일치하는 항목을 탐색할 수 있습니다. 새 창에서 검색 결과를 보려면 **찾기 2에 표시**를 선택합니다.  
  
#### <a name="to-replace-across-multiple-files-or-folders"></a>여러 파일이나 폴더에서 바꾸려면  
  
1.  **편집** 메뉴에서 **찾기 및 바꾸기** 를 가리킨 다음 **파일에서 바꾸기**를 클릭합니다.  
  
2.  **찾을 내용** 입력란에 검색할 텍스트를 입력합니다.  
  
3.  **바꿀 내용** 상자에 검색 텍스트를 바꿀 텍스트를 입력합니다.  
  
4.  **찾는 위치** 목록에서 **모든 열린 문서**, **현재 프로젝트**또는 **전체 솔루션**을 클릭하거나 디렉터리 경로를 입력합니다.  
  
5.  **바꾸기** 를 클릭하여 현재 검색 조건과 일치하는 항목을 **바꿀 내용** 상자에 있는 텍스트로 바꿉니다. **다음 찾기** 를 클릭하여 일치하는 항목 하나를 건너뛰거나 **파일 건너뛰기**를 클릭하여 전체 파일을 건너뛸 수 있습니다.  
  
     \- 또는-  
  
     **모두 바꾸기** 를 클릭하여 현재 검색 조건과 일치하는 모든 항목을 **바꿀 내용** 상자에 있는 텍스트로 바꿉니다. 나중에 바꾼 내용 중 일부를 실행 취소하려면 **모두 바꾸기를 실행한 후 수정한 파일 열어 두기** 를 선택합니다.  
  
    > [!NOTE]  
    >  **모두 바꾸기** 는 **파일 건너뛰기** 또는 **다음 찾기**로 건너뛴 파일의 일치하는 항목을 비롯하여 검색 조건과 일치하는 모든 항목을 바꿉니다. 바꾸기 작업 후에 계속 열려 있는 파일에서 수행된 바꾸기에 대해서만 **실행 취소** 를 사용할 수 있습니다.  
  
 기본적으로 찾기 결과 1 창에 바꾸기 정보가 표시됩니다. 찾기 결과 1 창에서 각 항목을 두 번 클릭하여 바꾸기 정보를 탐색할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [찾기 및 바꾸기](../../relational-databases/scripting/search-and-replace.md)   
 [대화형으로 문서 검색](../../relational-databases/scripting/search-documents-interactively.md)   
 [와일드카드로 텍스트 검색](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [정규식을 사용한 텍스트 검색](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
