---
title: 확장성 API
titleSuffix: Azure Data Studio
description: Azure Data Studio의 확장성 API에 대해 알아보기
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8a4ebe26cbbf768222c7b97b95fa7df238faded3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75001898"
---
# <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 확장성 API

[!INCLUDE[name-sos](../includes/name-sos.md)]는 확장 프로그램이 개체 탐색기와 같은 Azure Data Studio의 다른 부분과 상호 작용하는 데 사용할 수 있는 API를 제공합니다. 이러한 API는 [`src/sql/azdata.d.ts`](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/azdata.d.ts) 파일에서 사용할 수 있으며 아래에 설명되어 있습니다.

## <a name="connection-management"></a>연결 관리
`azdata.connection`

### <a name="top-level-functions"></a>최상위 함수

- `getCurrentConnection(): Thenable<azdata.connection.Connection>` 활성 편집기 또는 개체 탐색기 선택에 따라 현재 연결을 가져옵니다.

- `getActiveConnections(): Thenable<azdata.connection.Connection[]>` 활성 상태인 모든 사용자의 연결 목록을 가져옵니다. 이러한 연결이 없으면 빈 목록을 반환합니다.

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` 연결과 관련된 자격 증명이 포함된 사전을 가져옵니다. 이러한 항목은 `azdata.connection.Connection` 개체 아래에 있는 옵션 사전의 일부로 반환되지만 해당 개체에서 제거됩니다. 

### `Connection`
- `options: { [name: string]: string }` 연결 옵션의 사전입니다.
- `providerName: string` 연결 공급자의 이름(예: "MSSQL")입니다.
- `connectionId: string` 연결의 고유 식별자입니다.

### <a name="example-code"></a>코드 예
```
> let connection = azdata.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = azdata.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>개체 탐색기

`azdata.objectexplorer`


### <a name="top-level-functions"></a>최상위 함수
- `getNode(connectionId: string, nodePath?: string): Thenable<azdata.objectexplorer.ObjectExplorerNode>` 지정된 연결 및 경로에 해당하는 개체 탐색기 노드를 가져옵니다. 지정된 경로가 없는 경우 지정된 연결의 최상위 노드를 반환합니다. 지정된 경로에 노드가 없으면 `undefined`를 반환합니다. 참고: 개체의 `nodePath`는 SQL Tools 서비스 백 엔드에서 생성되며 직접 생성하기 어렵습니다. 향후 API 개선을 통해 이름, 유형 및 스키마와 같이 노드에 대해 제공하는 메타데이터를 기준으로 노드를 가져올 수 있습니다.

- `getActiveConnectionNodes(): Thenable<azdata.objectexplorer.ObjectExplorerNode>` 모든 활성 개체 탐색기 연결 노드를 가져옵니다.

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>` 지정된 메타데이터와 일치 하는 모든 개체 탐색기 노드를 찾습니다. `schema`, `database` 및 `parentObjectNames` 인수는 해당되지 않을 경우 `undefined`가 됩니다. `parentObjectNames`는 비데이터베이스 부모 개체의 목록으로, 개체 탐색기에서 가장 높은 수준부터 낮은 수준까지 포함되고 원하는 개체가 그 아래에 표시됩니다. 예를 들어 연결 ID가 `connectionId`이고, "schema1.table1" 테이블 및 "database1" 데이터베이스에 속하는 "column1" 열을 검색할 경우 `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`을 호출합니다. 이 API 호출에 대해 [Azure Data Studio가 기본적으로 지원하는 유형 목록](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API)도 참조하세요

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` 노드가 있는 연결의 ID입니다.

- `nodePath: string``getNode` 함수 호출에 사용되는 노드의 경로입니다.

- `nodeType: string` 노드 유형을 나타내는 문자열입니다.

- `nodeSubType: string` 노드의 하위 유형을 나타내는 문자열입니다.

- `nodeStatus: string` 노드의 상태를 나타내는 문자열입니다.

- `label: string` 개체 탐색기 표시되는 노드의 레이블입니다.

- `isLeaf: boolean` 노드가 리프 노드인지, 즉 자식이 없는지 여부입니다.

- `metadata: azdata.ObjectMetadata` 이 노드가 나타내는 개체를 설명하는 메타데이터입니다.

- `errorMessage: string` 노드가 오류 상태인 경우 표시되는 메시지입니다.

- `isExpanded(): Thenable<boolean>` 노드가 현재 개체 탐색기에서 확장되어 있는지 여부입니다.

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` 노드를 확장할지 또는 축소할지를 설정합니다. 상태를 None으로 설정하면 노드가 변경되지 않습니다.

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` 노드가 선택되어 있는지 여부를 설정합니다. `clearOtherSelections`가 true인 경우에는 새 항목을 선택할 때 다른 모든 항목을 선택 취소합니다. False이면 기존 선택을 유지합니다. `selected`가 true이면 `clearOtherSelections` 기본값은 true이고 `selected`가 false이면 false입니다.

- `getChildren(): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>` 이 노드의 모든 자식 노드를 가져옵니다. 자식이 없으면 빈 목록을 반환합니다.

- `getParent(): Thenable<azdata.objectexplorer.ObjectExplorerNode>` 이 노드의 부모 노드를 가져옵니다. 부모가 없으면 undefined를 반환합니다.

### <a name="example-code"></a>코드 예

```cs
private async interactWithOENode(selectedNode: azdata.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: azdata.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await azdata.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    azdata.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>제안된 API

확장을 통해 대화 상자, 마법사 및 설명서 탭에 사용자 지정 UI를 표시할 수 있도록 하기 위해 제안된 API를 추가했습니다. 이러한 API는 언제든지 변경할 수 있지만 [제안된 API 유형 파일](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/azdata.proposed.d.ts)에서 자세한 설명서를 참조하세요. 이러한 API 중 일부를 사용하는 방법의 예제는 ["sqlservices" 샘플 확장](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices)에서 찾을 수 있습니다.


