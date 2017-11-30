---
title: "REFRESH CUBE 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- REFRESH CUBE
- REFRESH_CUBE
- REFRESH
dev_langs: kbMDX
helpviewer_keywords:
- cubes [Analysis Services], cache
- refreshing cache
- REFRESH CUBE statement
- cache [Analysis Services]
ms.assetid: b8c087fb-5d17-4b13-b7cf-9929e9aab35c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 387b16e4d3570655b75bd548d6c2b5cd9e631d1b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX 데이터 정의-새로 고침 큐브
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  큐브에 대한 클라이언트 캐시를 새로 고칩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 인스턴스에 연결 하는 클라이언트 응용 프로그램에 대 한 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)],이 문을 사용 하면 서버와 동기화 할 클라이언트 응용 프로그램에 캐시 된 메모리입니다. 이 작업은 일반적으로 자동으로 감지되고 업데이트되지만 이 작업이 수행되기 전까지의 시간은 클라이언트 연결 문자열 설정에 따라 달라집니다. REFRESH CUBE 문은 데이터를 즉시 새로 고칩니다.  
  
 로컬 큐브에 연결된 클라이언트 응용 프로그램에 대해 REFRESH CUBE 문은 로컬 큐브 파일이 다시 작성되도록 합니다.  
  
> [!IMPORTANT]  
>  서버에 저장된 명명된 집합은 새로 고쳐지지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
