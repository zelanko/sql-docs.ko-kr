---
title: 모델 관리 (SQL Server 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, importing
- mining models, deleting
- mining models, managing
- mining models, training
- mining models, processing
- mining models, exporting
ms.assetid: c11380f0-7c24-4668-9cdf-9c53e4aff665
author: minewiskan
ms.author: owend
ms.openlocfilehash: f37939fea1188c18079fc7e619cee6a336876e24
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541855"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>모델 관리(SQL Server 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본, 모델 관리 단추](media/dmc-manage.gif "데이터 마이닝 리본, 모델 관리 단추")  
  
 **모델 관리** 대화 상자를 사용 하면 현재 연결 되어 있는 서버에 저장 된 기존 마이닝 모델 및 마이닝 구조와 상호 작용할 수 있습니다 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . 또한 현재 세션 중에 만든 임시 구조 및 모델을 보고 관리할 수도 있습니다. 세션 모델 및 서버에 저장된 모델을 모두 사용한 경우 둘 다 대화 상자에 표시됩니다.  
  
## <a name="using-the-manage-models-wizard"></a>모델 관리 마법사 사용  
 **모델 관리**를 클릭 하면 기존 데이터 마이닝 모델 및 구조를 관리 하는 다음 기능에 대 한 액세스를 제공 하는 **마이닝 구조 및 모델 관리** 대화 상자가 열립니다.  
  
-   마이닝 모델 또는 구조 이름 바꾸기  
  
-   마이닝 모델 또는 구조 삭제  
  
-   마이닝 모델 또는 구조 지우기  
  
-   새 데이터 또는 기존 데이터를 사용하여 마이닝 구조 처리  
  
-   마이닝 모델 또는 구조 내보내기 또는 가져오기  
  
> [!NOTE]  
>  이 대화 상자를 사용하여 쿼리 또는 모델을 만들 수는 없습니다. 새 마이닝 구조를 만들려면 Excel 용 데이터 마이닝 클라이언트에서 제공 하는 마법사 중 하나를 사용 하거나 **데이터 마이닝 쿼리 고급 편집기**를 사용 합니다.  
  
### <a name="requirements"></a>요구 사항  
 데이터 마이닝 모델을 관리하려면 먼저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결해야 합니다. 임시 파일에 저장된 세션 모델을 사용하는 경우에도 연결이 필요합니다. 연결을 만들거나 변경 하는 방법에 대 한 자세한 내용은 [Excel 용 데이터 마이닝 클라이언트&#41;&#40;원본 데이터에 연결 ](connect-to-source-data-data-mining-client-for-excel.md)을 참조 하세요.  
  
 연결하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 기존 데이터 마이닝 구조 또는 데이터 마이닝 모델이 없는 경우 이 추가 기능에서 제공하는 마법사 및 다른 도구를 사용하여 새로 만들 수 있습니다. **고급 편집기 데이터 마이닝 모델**을 사용 하 여 새 모델을 만들 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Excel 용 데이터 마이닝 추가 기능 &#40;마이닝 모델 문서화&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [Excel 용 데이터 마이닝 추가 기능 &#40;마이닝 모델 배포 및 확장&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
