---
title: 전역 설정 (로깅) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d314a2ca-ea2e-46e0-ae5e-8774841da91b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7d632b040a5124d73470ce825af91e254866a0ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299214"
---
# <a name="global-settings-logging-db2tosql"></a>전역 설정 (로깅) (DB2ToSQL)
사용 된 **전역 설정** SSMA에 대 한 로깅 설정을 지정 하려면 대화 상자. 일반적으로 기술 지원 서비스를 사용 하는 경우에 이러한 설정을 변경할는 있습니다.  
  
이 대화 상자에 액세스 하는 **도구** 메뉴에서 **전역 설정** 클릭 하 고는 **로깅** 왼쪽 창의 맨 아래에 있는 단추.  
  
## <a name="options"></a>변수  
**메시지 수준**  
다음 옵션을 사용할 수 있습니다 **메시지 수준**:  
  
|옵션|Description|  
|----------|---------------|  
|**[모든 범주]**|다음 옵션을 모두에 대 한 로깅 수준을 설정 하는 데 사용 합니다.|  
|**수집기**|소스 스키마에 대 한 메타 데이터를 수집 하 고 프로젝트에 저장 합니다.|  
|**변환기**|테이블 및 저장된 프로시저와 같은 원본 데이터베이스 개체의 구조에 해당 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구조입니다.|  
|**데이터 migrator**|원본 데이터베이스에서 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**포맷터**|에 대 한 스크립트를 생성 하는 변환기의 하위 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마입니다.|  
|**그래픽 사용자 인터페이스**|SSMA 도구를 사용할 때 나타나는 메시지입니다.|  
|**Linker**|SQL 식별자를 확인 하 고 다른 구성 요소에 대 한 정보를 제공 합니다.|  
|**기타**|다른 범주에 없는 모든 메시지입니다.|  
|**파서**|소스 스키마를 구문 분석합니다.|  
|**동기화**|로드에 대 한 데이터베이스 개체를 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**TreeConverter**|개체에 원본 메타 데이터에서 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터입니다.|  
|**테스터**|SSMA 테스터를 사용 하는 경우 나타나는 메시지입니다.|  
  
아래에 있는 각 옵션에 대 한 **메시지 수준**, SSMA에 대 한 다음 로깅 수준 중 하나를 구성 합니다.  
  
|||  
|-|-|  
|**심각한 오류**|심각한 오류 메시지만 로그에 작성 합니다.|  
|**오류**|로그에 오류 및 심각한 오류 메시지를 작성 합니다.|  
|**경고**|로그에 경고, 오류 및 심각한 오류 메시지를 작성 합니다.|  
|**Info**|로그에 정보, 경고, 오류 및 심각한 오류 메시지를 작성 합니다.|  
|**디버그**|디버그 로그에 메시지를 비롯 한 모든 메시지를 작성 합니다.|  
  
**로그 파일 경로**  
파일 경로 및 SSMA 로그 파일의 이름입니다. 다른 이름을 지정 하는 현재 경로 클릭 한 다음 찾아보기를 클릭 ( **...** ) 단추입니다.  
  
**로그 파일 크기**  
최대 크기 (kb)에서 로그 파일입니다. 최소 크기는 10KB입니다. 기본값은 10240KB 합니다.  
  
**로그 파일의 총 수**  
하나의 로그 차면 SSMA는 로그 파일 이름을 바꾸고 새로 시작 합니다. 이 설정을 사용 하 여 보관할 로그 파일의 최대 수를 지정 합니다. 최소값은 2입니다.  
  
