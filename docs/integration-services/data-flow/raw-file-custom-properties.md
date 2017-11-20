---
title: "원시 파일 사용자 지정 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a364ae62ebc8823f9d57fb44ef99b7b14469c608
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="raw-file-custom-properties"></a>원시 파일 사용자 지정 속성
  **원본 사용자 지정 속성**  
  
 원시 파일 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 원시 파일 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|원시 데이터에 액세스하는 데 사용되는 모드입니다. 가능한 값은 **파일 이름** (0) 및 **변수를 사용한 파일 이름** (1)입니다. 기본값은 **파일 이름** (0)입니다.|  
|FileName|문자열|원본 파일의 경로 및 파일 이름입니다.|  
  
 원시 파일 원본의 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Raw File Source](../../integration-services/data-flow/raw-file-source.md)을 참조하세요.  
  
 **대상 사용자 지정 속성**  
  
 원시 파일 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 원시 파일 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|FileName 속성에 파일 이름이 포함되어 있는지, 아니면 파일 이름이 포함된 변수의 이름이 포함되어 있는지를 지정하는 값입니다. 옵션은 **파일 이름** (0) 및 **변수를 사용한 파일 이름** (1)입니다.|  
|FileName|문자열|원시 파일 대상에서 쓰는 파일의 이름입니다.|  
|WriteOption|Integer(열거형)|원시 파일 대상에서 이름이 같은 기존 파일을 삭제하는지 여부를 지정하는 값입니다. 옵션은 **항상 만들기** (0), **한 번 만들기** (1), **잘라내기 및 추가** (3), **추가** (2)입니다. 이 속성의 기본값은 **항상 만들기** (0)입니다.|  
  
> [!NOTE]  
>  추가 작업을 수행하려면 추가된 데이터의 메타데이터가 파일에 이미 있는 데이터의 메타데이터와 일치해야 합니다.  
  
 원시 파일 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

