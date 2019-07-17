---
title: DELETE TAG 명령 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576e7e10d9d6f5c7e8616f57bde2dfed05503eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112067"
---
# <a name="delete-tag-command"></a>DELETE TAG 명령
복합 인덱스 (.cdx) 파일에서 태그 또는 태그를 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>인수  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]] ...  
 복합 인덱스 파일에서 제거할 태그를 지정 합니다. 쉼표로 구분 된 태그 이름 목록을 포함 하 여 삭제할 태그 하나를 사용 하 여 여러 태그를 삭제할 수 있습니다. 같은 이름의 두 개 이상의 태그 열린 인덱스 파일에 있는 경우에서 제거할 수 있습니다 태그는 특정 인덱스 파일의 포함 하 여 *CDXFileName*합니다.  
  
 모든 [OF *CDXFileName*]  
 복합 인덱스 파일에서 모든 태그를 제거합니다. 현재 테이블에는 구조적 복합 인덱스 파일이 있는 경우 인덱스 파일에서 모든 태그가 제거 됩니다, 인덱스 파일이 디스크에서 삭제 됩니다 및 관련된 구조 복합 인덱스 파일의 유무를 나타내는 테이블의 머리글에 플래그가 제거 됩니다. 모든 사용 *CDXFileName* 구조적 복합 인덱스 파일이 아닌 다른 복합 인덱스를 열고 파일에서 모든 태그를 제거 합니다.  
  
## <a name="remarks"></a>설명  
 복합 인덱스를 사용 하 여 만든 인덱스 파일, 인덱스 항목에 해당 하는 태그를 포함 합니다. 복합 인덱스를 열고 파일에서 태그 또는 태그를 제거 하려면 태그 삭제 됩니다. 복합 인덱스는 현재 작업 영역에 열려 있는 파일에서만 태그를 삭제할 수 있습니다. 복합 인덱스 파일에서 모든 태그를 제거 하면 디스크에서 파일이 삭제 됩니다.  
  
 Visual FoxPro 찾습니다 (열려 있으면) 구조적 복합 인덱스 파일의 태그에 대 한 첫 번째입니다. 태그 구조적 복합 인덱스 파일에 없는 경우 Visual FoxPro 다른 복합 인덱스를 열고 파일의 태그 다음 찾습니다.  
  
## <a name="see-also"></a>관련 항목  
 [INDEX 명령](../../odbc/microsoft/index-command.md)
