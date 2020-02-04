---
title: 파일 확장명을 코드 편집기에 연결
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- file extensions [SQL Server]
- associating file extensions [SQL Server]
- Query Editor [SQL Server Management Studio], associating file extensions
ms.assetid: 193630f4-93de-4950-8f36-68702531f925
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1e8b9084ff83c16c57241f737ccc40665ee2414b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75246463"
---
# <a name="associate-file-extensions-to-a-code-editor"></a>파일 확장명을 코드 편집기에 연결

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

파일 확장명을 특정 코드 편집기에 연결하면 Windows 탐색기에서 파일을 두 번 클릭하여 해당 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 코드 편집기에서 파일을 열 수 있습니다. .sql 및 .mdx와 같이 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 많이 사용되는 확장명은 설치 중에 연결됩니다. 새 파일 확장명은 파일 시스템에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에 연결해야 합니다. 이 기능을 사용하여 다른 편집기로 만든 파일을 열거나 .sql 파일의 백업인 .bak 파일과 같이 이름이 바뀐 파일을 열 수 있습니다.  
  
 이 과정은 두 단계로 구성됩니다. 먼저 확장명을 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]와 연결한 다음 해당 확장명을 특정 코드 편집기에 연결합니다.  
  
### <a name="to-associate-a-new-file-extension-with-sql-server-management-studio"></a>새 파일 확장명을 SQL Server Management Studio와 연결하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **보조프로그램**을 차례로 가리키고 **Windows 탐색기**를 클릭합니다.  
  
2.  Windows 탐색기의 **도구** 메뉴에서 **폴더 옵션**을 클릭합니다.  
  
3.  **폴더 옵션** 대화 상자에서 **파일 형식** 탭을 클릭하고 **새로 만들기**를 클릭합니다.  
  
4.  **새 확장명 만들기** 대화 상자의 **파일 확장명** 상자에 연결하려는 새 파일 확장명을 입력한 다음 **확인**을 클릭합니다. 확장명 앞에 마침표를 입력하지 마십시오.  
  
5.  **등록된 파일 형식** 상자에서 새 확장명을 클릭하고 **변경**을 클릭합니다.  
  
6.  **연결 프로그램** 대화 상자에서 **SSMS - SQL Server Management Studio**를 클릭한 다음, **확인**을 클릭합니다.  
  
7.  **닫기** 를 클릭하여 **폴더 옵션** 대화 상자를 닫은 다음 Windows 탐색기를 닫습니다.  
  
### <a name="to-associate-a-new-file-extension-with-a-code-editor-in-sql-server-management-studio"></a>새 파일 확장명을 SQL Server Management Studio의 코드 편집기와 연결하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **텍스트 편집기**를 클릭하고 **파일 확장명**을 클릭합니다.  
  
3.  **확장명** 상자에 새 파일 확장명을 입력합니다.  
  
4.  **편집기** 상자에서 이 파일 형식을 열 때 사용할 코드 편집기를 클릭하고 **추가**를 클릭한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Ssms 유틸리티](../../tools/sql-server-management-studio/ssms-utility.md)  
  
  
