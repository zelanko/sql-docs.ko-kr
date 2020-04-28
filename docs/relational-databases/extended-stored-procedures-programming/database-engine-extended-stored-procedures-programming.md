---
title: 확장 저장 프로시저 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
author: rothja
ms.author: jroth
ms.openlocfilehash: 541f24693598d20925dd37d4970c6d9916945793
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032007"
---
# <a name="database-engine-extended-stored-procedures---programming"></a>데이터베이스 엔진 확장 저장 프로시저 프로그래밍
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 이전에는 개방형 Data Services를 사용하여 SQL Server가 아닌 데이터베이스 환경에 대한 게이트웨이와 같은 서버 애플리케이션을 작성했습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 개방형 Data Services API의 사용되지 않는 부분을 지원하지 않습니다. 원래 개방형 Data Services API 중 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여전히 지원되는 부분은 확장 저장 프로시저뿐이므로 API의 이름이 확장 저장 프로시저 API로 바뀌었습니다.  
  
 분산 쿼리 및 CLR 통합과 같은 보다 강력한 최신 기술이 등장하면서 확장 저장 프로시저 API 애플리케이션의 필요성이 크게 바뀌었습니다.  
  
> [!NOTE]  
>  기존 게이트웨이 애플리케이션이 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 opends60.dll을 사용하여 해당 애플리케이션을 실행할 수 없습니다. 게이트웨이 애플리케이션은 더 이상 지원되지 않습니다.  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>확장 저장 프로시저 및 CLR 통합  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 XP(확장 저장 프로시저)는 데이터베이스 애플리케이션 개발자가 [!INCLUDE[tsql](../../includes/tsql-md.md)]로 표현하기 어렵거나 작성할 수 없는 서버 쪽 논리를 작성할 수 있었던 유일한 메커니즘을 제공했습니다. CLR Integration은 이러한 저장 프로시저를 작성하는 보다 강력한 대체 방법을 제공합니다. 또한 CLR 통합을 사용할 경우 저장 프로시저의 형태로 작성되던 논리를 보다 효율적인 테이블 반환 함수로 표현할 수 있습니다. 테이블 반환 함수를 통해 함수에서 생성된 결과를 FROM 절에 포함하여 SELECT 문으로 쿼리할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합 개요](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)   
 [CLR 테이블 반환 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
