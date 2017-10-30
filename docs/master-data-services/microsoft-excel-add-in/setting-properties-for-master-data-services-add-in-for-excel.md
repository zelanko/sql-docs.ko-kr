---
title: "Excel용 Master Data Services 추가 기능의 속성 설정 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: c5055942c39ff3805fcdbdbd47f0b3d8e9e2489d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="setting-properties-for-master-data-services-add-in-for-excel"></a>Excel용 Master Data Services 추가 기능의 속성 설정
  Excel용 Master Data Services 추가 기능 설정은 MDS에서 Excel 추가 기능으로 데이터가 로드되는 방법 및 Excel 추가 기능에서 MDS로 데이터가 게시되는 방법을 결정합니다.  
  
 Excel 추가 기능에 대한 설정을 지정하려면 **Excel**을 열고 **마스터 데이터** 메뉴를 클릭한 다음 **설정**을 클릭합니다. Excel에 액세스할 수 있는 사용자는 누구나 이러한 설정을 변경할 수 있습니다. 이 설정은 Excel이 열려 있는 컴퓨터에 적용됩니다.  
  
## <a name="excel-add-in-settings"></a>Excel 추가 기능 설정  
  
||||  
|-|-|-|  
|탭 및 섹션|설정|Description|  
|설정: 게시|게시할 때 **게시 및 주석** 대화 상자 표시|**게시** 를 클릭한 후 모든 변경 내용에 대한 단일 주석을 입력하거나 각 변경 내용에 대한 개별 주석을 입력할 수 있도록 **게시 및 주석**대화 상자를 표시하려면 선택합니다.<br /><br /> **게시 및 주석** 대화 상자를 표시하지 않고 게시 프로세스가 시작되도록 지정하려면 선택을 취소합니다. 이 경우 주석을 입력할 수 없습니다.|  
|설정: 버전|버전 선택|Excel 추가 기능으로 로드할 마스터 데이터의 버전을 선택합니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **없음** 은 기본 버전을 설정하지 않습니다.<br /><br /> **내림차순** 은 가장 오래된 버전을 기본값으로 설정하고, **오름차순** 은 최신 버전을 기본값으로 설정합니다.|  
|설정: 로깅|자세한 로깅 설정|MDS에서 Excel 추가 기능으로 마스터 데이터를 로드하는 프로세스에 대한 로깅을 설정하여 서비스의 모든 명령에 대한 결과가 기록되도록 합니다.|  
|설정: 원격 분석|원격 분석 데이터 컬렉션 켜기|원격 분석을 켜서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Excel 추가 기능의 품질, 안정성 및 성능을 개선합니다.|  
|설정: 일괄 처리 크기|로드할 셀 수|MDS 서버에서 Excel로 로드되는 일괄 처리에서 로드할 셀 수(1,000개 단위)를 나타내는 숫자를 선택합니다. 기본값은 50,000셀입니다.|  
|설정: 일괄 처리 크기|게시할 셀 수|Excel에서 서버로 반환되는 일괄 처리에서 게시할 셀 수(1,000개 단위)를 나타내는 숫자를 선택합니다. 기본값은 50,000셀입니다.|  
|설정: 수신 허용 목록에 추가된 서버|모두 지우기|연결된 바로 가기 쿼리 파일이 열릴 때 안전한 것으로 지정된 연결 목록을 지우려면 클릭합니다.|  
|데이터: 필터|큰 데이터 집합에 대해 필터 경고 표시|MDS에서 Excel로 로드 중인 데이터 집합이 최대 행 또는 열 수를 초과하는 경우 경고를 표시하려면 클릭합니다.|  
|데이터: 필터|최대 행 수|로드 중인 행 수에 대한 임계값을 선택합니다. 이 임계값을 초과하면 필터 경고가 게시됩니다.|  
|데이터: 필터|최대 열 수|로드 중인 열 수에 대한 임계값을 선택합니다. 이 임계값을 초과하면 필터 경고가 게시됩니다.|  
|데이터: 셀 형식|색상 변경 시기: 특성 값 변경|MDS 리포지토리의 새 데이터로 Excel 추가 기능 테이블을 새로 고칠 때 셀의 특성 값이 변경될 경우 해당 셀의 색이 변경되도록 지정하려면 클릭합니다.|  
|데이터: 셀 형식|색상 변경 시기: 멤버 추가됨|MDS 리포지토리의 새 데이터로 Excel 추가 기능 테이블을 새로 고칠 때 새 멤버가 행에 추가될 경우 해당 행의 셀 색이 변경되도록 지정하려면 클릭합니다.|  
|데이터: 셀 형식|표시 형식|도메인 기반 특성의 값을 표시하기 위한 기본 형식을 선택합니다. 옵션은 코드 {Name}, 코드 및 이름 {Code}입니다.|  
  
  

