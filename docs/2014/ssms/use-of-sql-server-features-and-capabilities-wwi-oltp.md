---
title: 외부 도구에 대한 인수 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2365ec137329675e2cd88e7f5bf7e1781aa3308f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63280487"
---
# <a name="arguments-for-external-tools"></a>Arguments for External Tools
  인수는 **도구** 메뉴에서 외부 도구가 시작될 때 Studio 환경에서 값을 제공하는 변수입니다. **외부 도구** 대화 상자를 사용하여 메모장과 같은 외부 도구를 **도구** 메뉴에 추가할 수 있습니다.  
  
 다음 표에서는 외부 도구에 대한 인수를 나열합니다.  
  
|속성|인수|Description|  
|----------|--------------|-----------------|  
|**항목 경로**|$(ItemPath)|현재 원본의 전체 파일 이름(드라이브 + 경로 + 파일 이름으로 정의됨)이며 비원본 창이 활성화된 경우에는 비어 있음|  
|**항목 디렉터리**|$(ItemDir)|현재 원본의 디렉터리(드라이브 + 경로로 정의됨)이며 비원본 창이 활성화된 경우에는 비어 있음|  
|**항목 파일 이름**|$(ItemFilename)|현재 원본의 파일 이름(파일 이름으로 정의됨)이며 비원본 창이 활성화된 경우에는 비어 있음|  
|**항목 확장명**|$(ItemExt)|현재 원본의 파일 이름 확장명|  
|**현재 줄** <sup>1</sup>|$(CurLine)|편집기에서 커서의 현재 줄 위치|  
|**현재 열**1|$(CurCol)|편집기에서 커서의 현재 열 위치|  
|**현재 텍스트**1|$(CurText)|현재 텍스트이며 현재 커서 위치 아래의 단어 또는 단일 줄 선택 영역(있을 경우)|  
|**대상 경로**|$(TargetPath)|대상의 전체 파일 이름(드라이브 + 경로 + 파일 이름으로 정의됨)|  
|**대상 디렉터리**|$(TargetDir)|대상의 디렉터리|  
|**대상 이름**|$(TargetName)|대상의 파일 이름|  
|**대상 확장명**|$(TargetExt)|대상의 파일 이름 확장명|  
|**프로젝트 디렉터리**|$(ProjDir)|현재 프로젝트의 디렉터리(드라이브 + 경로로 정의됨)|  
|**프로젝트 파일 이름**|$(ProjFileName)|현재 프로젝트의 파일 이름(드라이브 + 경로 + 파일 이름으로 정의됨)|  
|**솔루션 디렉터리**|$(SolutionDir)|현재 솔루션의 디렉터리(드라이브 + 경로로 정의됨)|  
|**솔루션 파일 이름**|$(SolutionFileName)|현재 솔루션의 파일 이름(드라이브 + 경로 + 파일 이름으로 정의됨)|  
  
 <sup>1</sup> 현재 줄, 현재 열 또는 현재 텍스트는 상태 표시줄에 표시 된 텍스트 편집기의 커서 위치를 기반으로 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [외부 도구 대화 상자](external-tools-dialog-box.md)   
 [일반 사용자 인터페이스 요소](general-user-interface-elements.md)  
  
  
