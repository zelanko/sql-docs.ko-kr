---
title: 데이터 마이닝 서버에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9ca50a030fef65c9de02bc93dcd970df2686b0a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420394"
---
# <a name="connect-to-a-data-mining-server"></a>데이터 마이닝 서버에 연결
  ![연결 단추](media/misc-connection.gif "연결 단추")  
  
 클릭 합니다 **연결** 기존 연결을 선택 하거나 새 인스턴스에 연결을 만들려면 단추 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다.  
  
 **서버에 연결 해야 하는 이유는 합니까?**  
  
 연결을 만들면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에서 제공하는 데이터 마이닝 알고리즘을 사용하여 서버에 최적화된 처리 기능을 활용할 수 있습니다.  
  
 데이터나 결과는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스 또는 SQL Server 데이터베이스에 보관하지 않아도 됩니다. Excel 데이터 마이닝 추가 기능은 Excel에 저장된 데이터 또는 Excel 데이터 원본으로 연결하는 데이터에 대해서만 사용할 수 있습니다.  
  
## <a name="how-to-create-a-new-connection"></a>새 연결을 만드는 방법  
  
1.  클릭 합니다 **연결** 단추입니다.  
  
2.  에 **Analysis Services 연결** 대화 상자, 클릭 **새로 만들기**합니다.  
  
3.  에 **Analysis Services에 연결** 대화 상자에서 서버 이름을 입력 합니다.  
  
4.  인증 방법을 지정합니다.  
  
5.  데이터 마이닝 모델을 저장할 카탈로그나 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 지정합니다.  
  
    > [!NOTE]  
    >  데이터베이스를 아직 만들지 않은 경우 (기본값)을 사용하여 데이터베이스를 만든 다음 연결을 테스트할 수 있습니다. 그러나 기본 연결에는 마이닝 모델을 추가할 수 없습니다. 마이닝 모델을 만들려면 먼저 기존 데이터베이스에 대한 연결을 만들어야 합니다.  
  
6.  웹 서비스를 통해 서버에 연결하는 경우 해당 웹 서비스에서 요구하는 사용자 이름과 암호를 입력합니다.  
  
7.  새 연결의 이름을 입력합니다.  
  
8.  클릭 **연결 테스트** 서버를 사용할 수 있는지 확인 합니다.  
  
## <a name="troubleshooting-connections"></a>연결 문제 해결  
 이 섹션에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 연결에 대한 몇 가지 일반적인 질문에 대한 답변을 제시합니다.  
  
 **"연결이 찾을 수 없습니다." 라는 메시지가**  
  
 단추의 아래쪽 부분에 있는 텍스트를 표시 하는 경우 **연결 없음**에 대 한 연결을 만들지 않은 의미는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스 또는 연결 하지 못했습니다. Excel에서 Access을 비롯한 기타 원본의 데이터를 계속 사용할 수 있지만 데이터 마이닝 모델을 만들거나 예측 쿼리를 실행하려면 활성 연결이 필요합니다.  
  
 **가정 서버를 사용 하도록 권한이 없습니까?**  
  
 서버에 마이닝 모델을 저장할 수 있는 권한이 없는 경우나 데이터 마이닝을 테스트하고 작업 내용을 저장하지는 않으려는 경우에는 테이블 분석 도구를 사용하여 임시 데이터 구조와 임시 모델을 만들 수 있습니다. 여전히 서버에 임시 모델을 저장할 수 있도록 해야 합니다. 사용 하도록 설정 하려면 관리자에 게 문의 *세션 마이닝 모델* 서버의 합니다.  
  
 모델이 저장되도록 하려는 경우 임시 모델을 사용하는 옵션을 해제하거나 데이터 마이닝 클라이언트에서 마법사를 사용할 수 있습니다. 이 마법사는 서버의 모든 모델을 저장합니다. 모델이 저장된 데이터베이스에 대해 관리 액세스 권한이 필요하므로 관리자에게 특별히 추가 기능이 있는 마이닝 모델을 만들 수 있는 데이터베이스를 만들어 달라고 요청하십시오.  
  
 **연결이; 내 모든 작업 손실?**  
  
 서버에 대한 연결이 끊긴 경우 Excel에 저장되어 있으므로 결과 및 데이터가 손실됩니다. 하지만 몇몇 임시 모델을 만든 경우에는 얼마 안 가서 서버에서 해당 모델이 삭제됩니다. 따라서 연결을 일시적으로 손실 되 면 잠시 모델 삭제 되지는 않으며 아직  
  
 모든 보고서와 테이블이 Excel에 저장되기 때문에 생성된 데이터나 결과가 전혀 손실되지 않습니다.  
  
> [!NOTE]  
>  추가 기능이 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버와 통신하는 동안 서버나 네트워크에서 분리하지 마십시오. 예를 들어 모델을 만들고 있거나 데이터를 처리하고 있을 때 연결을 끊으면 안 됩니다. 이러한 경우 연결을 끊으면 데이터가 손상될 수 있습니다.  
  
 **Visio 도구를 사용 하 여 모델을 연결할 수 없습니다.**  
  
 Visio용 데이터 마이닝 템플릿은 임시 마이닝 모델 및 구조를 사용할 수 없습니다. 마이닝 모델의 다이어그램을 만들려면 해당 모델이 서버에 저장되어 있어야 합니다.  
  
 **연결의 사용을 모니터링 하려면 어떻게 해야 하나요?**  
  
 합니다 [추적 &#40;Excel 용 데이터 마이닝 클라이언트&#41; ](trace-data-mining-client-for-excel.md) 도구 추가 기능 및 지정된 된 서버 간의 모든 활동의 로그를 만듭니다.  
  
 세션 모델 모니터링을 사용 하려면 선택 합니다 **세션 모델 사용** 옵션을 **추적 프로그램** 대화 상자.  
  
 이 추적을 사용하면 모델과 구조가 만들어지는 동안 생성된 DMX 및 XMLA 명령을 볼 수 있습니다. 또한 Excel에서 결과와 보고서를 생성하기 위해 클라이언트에서 전송한 쿼리를 볼 수 있습니다.  
  
 **임시 모델 이란 무엇 인가요? 임시 모델을 저장 하려면 어떻게 해야 합니까?**  
  
 Excel용 테이블 분석 도구는 기본적으로 임시 데이터 구조 및 마이닝 모델을 만듭니다. 통합 문서가 열려 있고 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 연결되어 있는 동안 계속해서 임시 모델을 찾아보고 쿼리할 수 있습니다.  
  
 Excel 통합 문서를 닫거나 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 연결을 변경 또는 종료하면 만들어진 구조 및 모델이 모두 삭제됩니다.  
  
 Excel용 데이터 마이닝 클라이언트에서 마법사를 완료하면 모델이 서버에 기본적으로 저장되지만, 각 마법사의 마지막 페이지에는 임시 모델을 사용하는 옵션이 있습니다. 이 옵션을 선택하면 사용자가 만든 데이터 마이닝 구조 및 모델이 임시 파일에 저장됩니다. Excel이 열려 있는 동안 구조 및 모델을 찾아보기, 관리 및 수정할 수 있지만 Excel을 닫으면 구조와 관련 모델이 삭제됩니다.  
  
 사용 하 여 임시 구조 또는 모델을를 명시적으로 만들 수는 **데이터 마이닝 고급 쿼리 편집기** DMX 템플릿 중 하나를 선택 하 고 있습니다. `USE SESSION MODELS` 절을 추가하여 해당 개체를 임시로 지정합니다.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>마이닝 모델 및 구조 백업 만들기  
 모델 또는 구조의 백업을 만들려면 내보낼 수 있습니다 사용 하 여 [모델 관리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](manage-models-sql-server-data-mining-add-ins.md), Excel 용 데이터 마이닝 클라이언트에서.  
  
 임시 마이닝 모델을 만든 경우 일반적으로 Table5_593679_TS_62446와 같이 이해 하기 어려운 이름이 지정됩니다. 사용할 수 있습니다 합니다 [추적 &#40;Excel 용 데이터 마이닝 클라이언트&#41; ](trace-data-mining-client-for-excel.md) 임시 구조 및 테이블 분석 도구에서 생성 된 모델의 이름을 검색 하 고 다음을 사용 하 여 백업 도구를  **모델 관리**합니다.  
  
##### <a name="identify-and-export-a-temporary-model"></a>임시 모델 식별 및 내보내기  
  
1.  에 **연결** 데이터 마이닝 클라이언트의 그룹 Excel에 대 한 클릭 **추적**합니다.  
  
2.  연결 활동 로그를 확인하고 열 및 예측 가능 결과(예)를 검토하여 모델을 찾습니다.  
  
     고급 사용자: DMX 또는 XMLA에 대해 잘 알고 있는 경우 이 문을 나중에 사용할 수 있도록 파일에 복사할 수 있습니다.  
  
3.  임시 모델 및 구조 이름을 찾으면 엽니다 **모델 관리** 고 모델을 선택 합니다.  
  
4.  지정한 위치에서 스크립트 파일을 생성하려면 이 마이닝 모델 내보내기를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [원본 데이터에 연결 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [서버 구성 유틸리티 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
