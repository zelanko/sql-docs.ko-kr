---
title: 고급 개체 선택 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c978fba4-c953-4ed0-a21d-1b38e7225552
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: 01fcdf57e6c9b99537ab40ffa54db9e0414eebad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="advanced-object-selection--oracletosql"></a>고급 개체 선택 (OracleToSQL)
**고급 개체 섹션** 대화 상자를 사용 하면 개체 이름에 문자열 및 부분 문자열을 사용 하 여 데이터베이스 개체를 필터링 한 다음 선택 하거나 해당 개체를 선택 취소 합니다. SSMA는 선택한 개체에 변환 및 마이그레이션 작업을 수행합니다.  
  
이 대화 상자에 액세스 하려면 메타 데이터 탐색기에서 마우스 오른쪽 단추로 클릭 한 다음 선택 **고급 개체 선택**합니다.  
  
대화 상자를 처음 열 때 클릭 **하위 항목 표시** 프로젝트에 로드 하는 메타 데이터에 있는 모든 개체를 표시 합니다. 다음 항목을 필터링 하는 문자열을 입력할 수 있습니다. 예를 들어 "company" 이름이 해당 문자열을 포함 하는 모든 항목을 표시할 문자열을 입력 합니다.  
  
이 대화 상자를 사용 하기 전에를 강제로 SSMA 스키마 변환 하거나 프로젝트를 저장 하 여 모든 메타 데이터를 로드 하는 것이 좋습니다.  
  
## <a name="options"></a>옵션  
**모든 항목 선택**  
모든 항목 옆에 있는 확인 표시를 추가합니다. 메타 데이터 탐색기에서 이러한 항목을 즉시 선택 됩니다.  
  
**모든 항목을 선택 취소**  
모든 항목 옆의 확인 표시를 제거합니다. 이러한 항목은 메타 데이터 탐색기에 즉시 해제 됩니다.  
  
**목록 뷰 모드**  
표시 목록에서 항목을 필터링 합니다.  
  
**테이블 보기 모드**  
표시는 테이블에 있는 항목을 필터링합니다.  
  
**만 로드 된 항목 표시**  
범주 또는 항목의 표시를 전환합니다. 이 단추를 선택 하는 경우 SSMA 필터 조건 및 이전에 로드 된 하는 일치 하는 모든 항목을 표시 합니다. 이 단추를 선택 하지 않으면 범주 폴더 SSMA를 보여 줍니다.  
  
**필터**  
항목을 필터링 하는 데 사용할 문자열을 입력 합니다. 예를 들어 찾으려면 문자열이 포함 된 사용 가능한 모든 항목 "ID" 항목 이름에을 입력 문자열 "ID"에 **필터** 상자입니다.  
  
필터 조건과 일치 하는 항목, 문자열을 입력할 때 범주 또는 항목이 표시 됩니다. 일치 하는 항목을 보려면 클릭 하면 권장는 **로드 항목만 표시** 단추입니다.  
  
**필터 지우기**  
지웁니다는 **필터** 상자입니다.  
  
