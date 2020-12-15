---
title: Azure Data Studio에서 Kqlmagic(Kusto 쿼리 언어)을 사용하여 Notebook 만들기
description: 이 자습서에서는 Azure Data Studio에서 Kqlmagic을 만들고 실행하는 방법을 보여 줍니다.
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 10/29/2020
ms.openlocfilehash: cdb110059043741627300e1f6d080582363d834b
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96900836"
---
# <a name="kqlmagic-in-azure-data-studio"></a>Azure Data Studio의 Kqlmagic

**Kqlmagic** 은 **[Azure Data Studio Notebook](./notebooks-guidance.md)** 에서 Python 커널의 기능을 확장하는 명령입니다. Python과 **[KQL(Kusto 쿼리 언어)](/azure/data-explorer/kusto/query)** 을 결합하여, `render` 명령이 통합된 Plot.ly 라이브러리를 사용하여 데이터를 쿼리하고 시각화할 수 있습니다. Kqlmagic은 하나의 위치에서 Notebook, 데이터 분석 및 풍부한 Python 기능이라는 장점을 제공합니다. Kqlmagic이 지원되는 데이터 원본에는 **[Azure Data Explorer](/azure/data-explorer/data-explorer-overview)** , **[Application Insights](/azure/azure-monitor/app/app-insights-overview)** , **[Azure Monitor 로그](/azure/azure-monitor/platform/data-platform-logs)** 등이 있습니다.

이 문서에서는 Azure Data Studio에서 Azure Data Explorer 클러스터, Application Insights 로그 및 Azure Monitor 로그용 Kqlmagic 확장을 사용하여 Notebook을 만들고 실행하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

- [Azure Data Studio](../download-azure-data-studio.md)
- [Python](https://www.python.org/downloads/)

## <a name="install-and-set-up-kqlmagic-in-a-notebook"></a>Notebook에서 Kqlmagic 설치 및 설정

이 섹션의 단계는 모두 Azure Data Studio Notebook에서 실행됩니다.

1. 새 Notebook을 만들고 **커널** 을 *Python 3* 으로 변경합니다.

   ![새 Notebook](media/notebooks-kqlmagic/install-new-notebook.png)

2. 메시지가 표시되면 **예** 를 선택하여 Python 패키지를 업그레이드합니다.

   ![예](media/notebooks-kqlmagic/install-python-yes.png)

3. Kqlmagic을 설치합니다.

   ```python
   !pip install Kqlmagic --no-cache-dir --upgrade
   ```

   설치되었는지 확인합니다.

   ```python
   !pip list
   ```

   ![목록](media/notebooks-kqlmagic/install-list.png)

4. Kqlmagic을 로드합니다.

   ```python
   %reload_ext Kqlmagic
   ```

   > [!Note]
   > 이 단계가 실패하면 파일을 닫고 다시 엽니다.

   ![Kqlmagic 확장 로드](media/notebooks-kqlmagic/install-load-kql-magic-ext.png)

5. 도움말 설명서를 살펴보거나 버전을 확인하여 Kqlmagic이 올바르게 로드되었는지 테스트할 수 있습니다.

   ```python
   %kql --help "help"
   ```

   > [!Note]
   > `Samples@help`에서 암호를 요구하는 경우 공란으로 두고 **Enter** 키를 누르면 됩니다.

   ![도움말](media/notebooks-kqlmagic/install-help.png)

   설치된 Kqlmagic 버전을 확인하려면 다음 명령을 실행합니다.

   ```python
   %kql --version
   ```

## <a name="kqlmagic-with-an-azure-data-explorer-cluster"></a>Azure Data Explorer 클러스터와 Kqlmagic

이 섹션에서는 Azure Data Explorer 클러스터에서 Kqlmagic을 사용하여 데이터 분석을 실행하는 방법을 설명합니다.

### <a name="load-and-authenticate-kqlmagic-for-azure-data-explorer"></a><a name="ade-load-auth"></a> Azure Data Explorer용 Kqlmagic 로드 및 인증

   > [!Note]
   > Azure Data Studio에서 새 Notebook을 만들 때마다 Kqlmagic 확장을 로드해야 합니다.

1. **커널** 이 *Python3* 으로 설정되었는지 확인합니다.

   ![커널 변경](media/notebooks-kqlmagic/change-kernel.png)

2. Kqlmagic을 로드합니다.

   ```python
   %reload_ext Kqlmagic
   ```

   ![Kqlmagic 확장 로드](media/notebooks-kqlmagic/install-load-kql-magic-ext.png)

3. 클러스터에 연결하고 인증합니다.

   ```python
   %kql azureDataExplorer://code;cluster='help';database='Samples'
   ```

    > [!Note]
    > 고유의 ADX 클러스터를 사용하는 경우 다음과 같이 연결 문자열에서 지역을 포함해야 합니다.   
    ```%kql azuredataexplorer://code;cluster='mycluster.westus';database='mykustodb'```

   인증에는 디바이스 로그인을 사용합니다. 출력에서 코드를 복사하고 **인증** 을 선택하면 열리는 브라우저에 코드를 붙여넣습니다. 인증에 성공하면 Azure Data Studio로 돌아가서 스크립트의 나머지 부분을 계속 진행할 수 있습니다.

   ![Azure Data Explorer 인증](media/notebooks-kqlmagic/ade-auth.png)

### <a name="query-and-visualize-for-azure-data-explorer"></a>Azure Data Explorer에 대해 쿼리 및 시각화

[렌더링 연산자](/azure/data-explorer/kusto/query/renderoperator)를 사용하여 데이터를 쿼리하고 ploy.ly 라이브러리를 사용하여 데이터를 시각화합니다. 이 쿼리 및 시각화는 네이티브 KQL을 사용하는 통합 환경을 제공합니다.

1. 주와 빈도를 기준으로 상위 10개의 폭풍우 이벤트를 분석합니다.

   ```python
   %kql StormEvents | summarize count() by State | sort by count_ | limit 10
   ```

   KQL(Kusto 쿼리 언어)에 익숙하다면, `%kql` 뒤에 쿼리를 입력할 수 있습니다.

   ![폭풍우 이벤트 분석](media/notebooks-kqlmagic/ade-analyze-storm-events.png)

2. 타임라인 차트를 시각화합니다.

   ```python
   %kql StormEvents \
   | summarize event_count=count() by bin(StartTime, 1d) \
   | render timechart title= 'Daily Storm Events'
   ```

   ![시간 차트 시각화](media/notebooks-kqlmagic/ade-visualize-timechart.png)

3. `%%kql`을 사용한 여러 줄의 쿼리입니다.

   ```python
   %%kql
   StormEvents
   | summarize count() by State
   | sort by count_
   | limit 10
   | render columnchart title='Top 10 States by Storm Event count'
   ```

   ![여러 줄의 쿼리 샘플](media/notebooks-kqlmagic/ade-multiline-query-sample.png)

## <a name="kqlmagic-with-application-insights"></a>Kqlmagic과 Application Insights

### <a name="load-and-authenticate-kqlmagic-for-application-insights"></a><a name="appin-load-auth"></a> Application Insights용 Kqlmagic 로드 및 인증

1. **커널** 이 *Python3* 으로 설정되었는지 확인합니다.

   ![커널](media/notebooks-kqlmagic/change-kernel.png)

2. Kqlmagic을 로드합니다.

   ```python
   %reload_ext Kqlmagic
   ```

   ![Kqlmagic 확장 로드](media/notebooks-kqlmagic/install-load-kql-magic-ext.png)

   > [!Note]
   > Azure Data Studio에서 새 Notebook을 만들 때마다 Kqlmagic 확장을 로드해야 합니다.

3. 연결 및 인증합니다.

   먼저 Application Insights 리소스의 API 키를 생성해야 합니다. 그런 다음 애플리케이션 ID 및 API 키를 사용하여 Notebook에서 Application Insights에 연결합니다.

   ```python
   %kql appinsights://appid='DEMO_APP';appkey='DEMO_KEY'
   ```

### <a name="query-and-visualize-for-application-insights"></a>Application Insights에 대해 쿼리 및 시각화

[렌더링 연산자](/azure/data-explorer/kusto/query/renderoperator)를 사용하여 데이터를 쿼리하고 ploy.ly 라이브러리를 사용하여 데이터를 시각화합니다. 이 쿼리 및 시각화는 네이티브 KQL을 사용하는 통합 환경을 제공합니다.

1. 페이지 보기를 표시합니다.

   ```python
   %%kql
   pageViews
   | limit 10
   ```

   ![페이지 보기](media/notebooks-kqlmagic/appin-page-views.png)

   > [!Note]
   > 마우스를 사용하여 차트의 영역으로 끌어서 특정 날짜로 확대합니다.

2. 타임라인 차트에서 페이지 보기를 표시합니다.

   ```python
   %%kql
   pageViews
   | summarize event_count=count() by name, bin(timestamp, 1d)
   | render timechart title= 'Daily Page Views'
   ```

   ![타임라인 차트](media/notebooks-kqlmagic/appin-timechart.png)

## <a name="kqlmagic-with-azure-monitor-logs"></a>Kqlmagic과 Azure Monitor 로그

### <a name="load-and-authenticate-kqlmagic-for-azure-monitor-logs"></a><a name="aml-load-auth"></a> Azure Monitor 로그용 Kqlmagic 로드 및 인증

1. **커널** 이 *Python3* 으로 설정되었는지 확인합니다.

   ![변경](media/notebooks-kqlmagic/change-kernel.png)

2. Kqlmagic을 로드합니다.

   ```python
   %reload_ext Kqlmagic
   ```

   ![Kqlmagic 확장 로드](media/notebooks-kqlmagic/install-load-kql-magic-ext.png)

   > [!Note]
   > Azure Data Studio에서 새 Notebook을 만들 때마다 Kqlmagic 확장을 로드해야 합니다.

3. 연결 및 인증합니다.

   ```python
   %kql loganalytics://workspace='DEMO_WORKSPACE';appkey='DEMO_KEY';alias='myworkspace'
   ```

   ![Log Analytics 인증](media/notebooks-kqlmagic/aml-auth.png)

### <a name="query-and-visualize-for-azure-monitor-logs"></a>Azure Monitor 로그에 대해 쿼리 및 시각화

[렌더링 연산자](/azure/data-explorer/kusto/query/renderoperator)를 사용하여 데이터를 쿼리하고 ploy.ly 라이브러리를 사용하여 데이터를 시각화합니다. 이 쿼리 및 시각화는 네이티브 KQL을 사용하는 통합 환경을 제공합니다.

1. 타임라인 차트를 봅니다.

   ```python
   %%kql
   KubeNodeInventory
   | summarize event_count=count() by Status, bin(TimeGenerated, 1d)
   | render timechart title= 'Daily Kubernetes Nodes'
   ```

   ![Log Analytics 일일 Kubernetes 노드 시간 차트](media/notebooks-kqlmagic/aml-timechart-daily-kubernetes-nodes.png)

## <a name="next-steps"></a>다음 단계

Notebook 및 Kqlmagic에 대한 자세한 정보:

- [Azure Data Studio용 Kusto(KQL) 확장(미리 보기)](https://docs.microsoft.com/sql/azure-data-studio/extensions/kusto-extension)
- [Kusto(KQL) Notebook(미리 보기) 만들기 및 실행](https://docs.microsoft.com/sql/azure-data-studio/notebooks/notebooks-kusto-kernel)
- [Azure Data Explorer에서 Jupyter Notebook 및 kqlmagic 확장을 사용하여 데이터 분석하기](/azure/data-explorer/Kqlmagic)
- Kusto, Application Insights 및 LogAnalytics 데이터로 작업할 수 있는 Notebook 환경을 지원하는 [Jupyter Notebook 및 Jupyter Lab으로 확장(Magic)](https://github.com/Microsoft/jupyter-Kqlmagic).
- [Kqlmagic](https://pypi.org/project/Kqlmagic/)
- [Azure Data Studio에서 Notebook을 사용하는 방법](./notebooks-guidance.md)
