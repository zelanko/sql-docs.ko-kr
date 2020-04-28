---
title: 전역 설정 (로깅) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 835b09b5-eb42-47ea-b46e-e115d4d6461f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 72efa0f050a3b930ebaa99ff425b48e1fe9b6ba5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67986646"
---
# <a name="global-settings-logging-accesstosql"></a>전역 설정 (로깅) (AccessToSQL)
**전역 설정** 대화 상자를 사용 하 여 ssma의 로깅 설정을 지정할 수 있습니다. 일반적으로 제품 지원에 대 한 작업을 수행 하는 경우에만 이러한 설정을 변경할 수 있습니다.  
  
이 대화 상자에 액세스 하려면 **도구** 메뉴에서 **전역 설정** 을 선택 하 고 왼쪽 창의 맨 아래에 있는 **로깅** 단추를 클릭 합니다.  
  
## <a name="options"></a>옵션  
**메시지 수준**  
**메시지 수준**에서 사용할 수 있는 옵션은 다음과 같습니다.  
  
|옵션|설명|  
|----------|---------------|  
|**[모든 범주]**|다음 옵션에 대 한 로깅 수준을 설정 하는 데 사용 됩니다.|  
|**데이터 수집기**|소스 스키마에 대 한 메타 데이터를 수집 하 여 프로젝트에 저장 합니다.|  
|**변환기**|테이블 및 저장 프로시저와 같은 원본 데이터베이스 개체의 구조를 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구조체로 변환 합니다.|  
|**데이터 migrator**|원본 데이터베이스에서로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터를 마이그레이션합니다.|  
|**포맷터**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마에 대 한 스크립트를 생성 하는 변환기의 하위 구성 요소입니다.|  
|**그래픽 사용자 인터페이스**|SSMA 도구를 사용할 때 표시 되는 메시지입니다.|  
|**링커**|SQL 식별자를 확인 하 고 다른 구성 요소에 정보를 제공 합니다.|  
|**기타**|다른 범주에 없는 모든 메시지|  
|**파서**|소스 스키마를 구문 분석 합니다.|  
|**장치의**|원본 데이터베이스 개체를에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로드 합니다.|  
|**TreeConverter**|원본 메타 데이터의 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터로 변환 합니다.|  
  
각 옵션의 **메시지 수준**에서 ssma에 대해 다음 로깅 수준 중 하나를 구성 합니다.  
  
|||  
|-|-|  
|**심각한 오류**|심각한 오류 메시지를 로그에 기록 합니다.|  
|**오류**|로그에 오류 및 심각한 오류 메시지를 씁니다.|  
|**내용의**|로그에 경고, 오류 및 심각한 오류 메시지를 기록 합니다.|  
|**정보**|정보, 경고, 오류 및 심각한 오류 메시지를 로그에 기록 합니다.|  
|**디버그**|디버그 메시지를 포함 하 여 모든 메시지를 로그에 씁니다.|  
  
**로그 파일 경로**  
SSMA 로그 파일의 파일 경로 및 이름입니다. 다른 이름을 지정 하려면 현재 경로를 클릭 한 다음 찾아보기 (**...**) 단추를 클릭 합니다.  
  
**로그 파일 크기**  
로그 파일의 최대 크기 (KB)입니다. 최소 크기는 10kb입니다. 기본 크기는 10240 KB입니다.  
  
**총 로그 파일 수**  
한 로그가 채워지면 SSMA는 로그 파일의 이름을 바꾸고 새 파일을 시작 합니다. 이 설정을 사용 하 여 유지할 최대 로그 파일 수를 지정 합니다. 최소값은 2입니다.  
  
