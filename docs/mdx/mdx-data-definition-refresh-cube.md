---
title: REFRESH CUBE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 957609573c206b7c3492789c369d0fb2be2398a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038166"
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
 인스턴스에 연결 하는 클라이언트 응용 프로그램에 대 한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)],이 문을 사용 하면 서버와 동기화 되도록 클라이언트 응용 프로그램에 캐시 된 메모리입니다. 이 작업은 일반적으로 자동으로 감지되고 업데이트되지만 이 작업이 수행되기 전까지의 시간은 클라이언트 연결 문자열 설정에 따라 달라집니다. REFRESH CUBE 문은 데이터를 즉시 새로 고칩니다.  
  
 로컬 큐브에 연결된 클라이언트 응용 프로그램에 대해 REFRESH CUBE 문은 로컬 큐브 파일이 다시 작성되도록 합니다.  
  
> [!IMPORTANT]  
>  서버에 저장된 명명된 집합은 새로 고쳐지지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
