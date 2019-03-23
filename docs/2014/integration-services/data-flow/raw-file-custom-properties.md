---
title: 원시 파일 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe3f77ac629aab7534077274aa9cf62a50149b57
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376271"
---
# <a name="raw-file-custom-properties"></a>원시 파일 사용자 지정 속성
  **원본 사용자 지정 속성**  
  
 원시 파일 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 원시 파일 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|원시 데이터에 액세스하는 데 사용되는 모드입니다. 가능한 값은 `File name`(0) 및 `File name from variable`(1)입니다. 기본값은 `File name`(0)입니다.|  
|FileName|문자열|원본 파일의 경로 및 파일 이름입니다.|  
  
 원시 파일 원본의 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Raw File Source](raw-file-source.md)을 참조하세요.  
  
 **대상 사용자 지정 속성**  
  
 원시 파일 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 원시 파일 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|FileName 속성에 파일 이름이 포함되어 있는지, 아니면 파일 이름이 포함된 변수의 이름이 포함되어 있는지를 지정하는 값입니다. 옵션으로는 `File name`(0) 및 `File name from variable`(1)이 있습니다.|  
|FileName|문자열|원시 파일 대상에서 쓰는 파일의 이름입니다.|  
|WriteOption|Integer(열거형)|원시 파일 대상에서 이름이 같은 기존 파일을 삭제하는지 여부를 지정하는 값입니다. 옵션으로는 `Create Always`(0), `Create Once`(1), `Truncate and Append`(3) 및 `Append`(2)가 있습니다. 이 속성의 기본값은 `Create Always`(0)입니다.|  
  
> [!NOTE]  
>  추가 작업을 수행하려면 추가된 데이터의 메타데이터가 파일에 이미 있는 데이터의 메타데이터와 일치해야 합니다.  
  
 원시 파일 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Raw File Destination](raw-file-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [공용 속성](../common-properties.md)  
  
  
