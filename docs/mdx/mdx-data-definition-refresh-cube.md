---
description: MDX 데이터 정의 - REFRESH CUBE
title: REFRESH CUBE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05ae95c97ae21d3b8ff7b4e457cf3ddf8cc38989
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387057"
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX 데이터 정의 - REFRESH CUBE


  큐브에 대한 클라이언트 캐시를 새로 고칩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 인스턴스에 연결 된 클라이언트 응용 프로그램의 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이 문은 클라이언트 응용 프로그램에 캐시 된 메모리가 서버와 동기화 되도록 합니다. 이 작업은 일반적으로 자동으로 감지되고 업데이트되지만 이 작업이 수행되기 전까지의 시간은 클라이언트 연결 문자열 설정에 따라 달라집니다. REFRESH CUBE 문은 데이터를 즉시 새로 고칩니다.  
  
 로컬 큐브에 연결된 클라이언트 애플리케이션에 대해 REFRESH CUBE 문은 로컬 큐브 파일이 다시 작성되도록 합니다.  
  
> [!IMPORTANT]  
>  서버에 저장된 명명된 집합은 새로 고쳐지지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 데이터 정의 문은 MDX를 &#40;&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
