## ð¡ é¢è§

æ°´å¹³å¸å± (master)ï¼https://epee.netlify.app/
![hlayout](https://raw.githubusercontent.com/dobble11/aseets/master/hlayout.png)

åç´å¸å± ([dev-vertical-layout](https://github.com/dobble11/epee-react-admin-ts/tree/dev-vertical-layout))ï¼https://vepee.netlify.app/
![vlayout](https://raw.githubusercontent.com/dobble11/aseets/master/vlayout.png)

## ð ç¹æ§

- é¶éç½®
- æ æ¨¡çä»£ç 
- ä½¿ç¨ React Hooks å¼å
- åºäº easy-peasy çç¶æç®¡ç
- å®åçç±»åæ£æ¥å lint è§åï¼ä¿è¯ä»£ç é£æ ¼çä¸è´åè´¨é
- docker é¨ç½²æ¯æ
- [å¨çº¿æ°æ® mock](https://github.com/dobble11/epee-react-admin-ts/blob/master/docs/ç®åçå¨çº¿æ°æ®mock.md)

## ð å¼å§

```sh
yarn
yarn start
```

> ä¸ºäºæ´å¥½çå¼åä½éªï¼ä½ è¿éè¦å®è£ä»¥ä¸ VSCode æä»¶
>
> - **Prettier - Code formatter**
> - **ESLint**
>
> æ¨èå®è£
>
> - **Auto Close Tag**
> - **Auto Import**
> - **Auto Rename Tag**
> - **CSS Modules**
> - **Paste JSON as Code**
> - **Path Intellisense**
> - **ES7 React/Redux/GraphQL/React-Native snippets**

## ð³ ç®å½ç»æ

```sh
âââ /.vscode/                    # vscode éç½®ç®å½ï¼åå«å¸¸ç¨çä»£ç çæ®µãè®¾ç½®ç­
âââ /@types/                     # å¨å±ç±»åå£°æ
âââ /src/                        # æºç ç®å½
â âââ /assets/                   # éæèµæºç®å½
â âââ /components/               # å¬å±ä¸å¡ç»ä»¶ç®å½
â âââ /constants/                # constant ç®å½
â â âââ _const.scss              # scss å¸¸é
â â âââ Api.ts                   # API å¸¸é
â â âââ store.ts                 # store
â â âââ router.ts                # è·¯ç±æ 
â âââ /hooks/                    # hook ç®å½
â âââ /layouts/                  # å¸å±ç®å½
â âââ /models/                   # æ¨¡åç®å½
â âââ /pages/                    # é¡µé¢ç»ä»¶ç®å½
â âââ /services/                 # è¯·æ±æå¡ç®å½
â âââ /style/                    # å¨å±æ ·å¼
â âââ /utils/                    # util ç®å½
â â âââ request.ts               # åºäº fetch å°è£ç http è¯·æ±å·¥å·
â â âââ global.ts                # å¬å±æ¹æ³åº
â âââ index.tsx                  # é¡¹ç®å¥å£
```

## â å¼å

### æ°å¢é¡µé¢

è¿éçãé¡µé¢ãæéç½®äºè·¯ç±ï¼è½å¤éè¿é¾æ¥ç´æ¥è®¿é®çæ¨¡å

#### 1. æ°å¢ tsxãscss æä»¶

```diff
src
  models
  pages
+   NewPage.tsx
+   NewPage.module.scss
```

**NewPage.tsx** é¨åä»£ç å¦ä¸ï¼

```tsx
export default function NewPage(props: NewPageProps) {
  return <div className={styles.wrap}>New Page</div>;
}
```

å¯ä»¥é®å¥ `tsrfc` å¿«éçææ¨¡æ¿ä»£ç ï¼åé¢ç´æ¥ååºä»£ç çæ®µå¿«æ·é®ï¼ä¸åè¯´æ

#### 2. å°é¡µé¢å å¥è·¯ç±

ä¿®æ¹ **constants/router.ts** åå®¹

```diff
export const router: RouteNode[] = [
  {
    path: '/dashboard',
    name: 'Dashboard',
    icon: DashboardOutlined,
    routes: [
      { path: '/dashboard/analysis', name: 'åæé¡µ', component: Analysis },
    ],
  },
  ...
+  {
+    path: '/new',
+    name: 'æ°é¡µé¢',
+    icon: FileOutlined,
+    component: NewPage,
+  },
]
```

ä¿®æ¹å¥½ä¹åè¿è¡ï¼å¯ä»¥çå°å¦ä¸ææ

![preview](https://raw.githubusercontent.com/dobble11/aseets/master/newpage.png)

### å¼å¥æ°æ®æµ

> ç¶æç®¡çä½¿ç¨ **easy-peasy**ï¼æ´å¤ç¨æ³åè[å®æ¹ææ¡£](https://easy-peasy.now.sh)

ä¸é¢æ¼ç¤ºè¡¨æ ¼ç»ä»¶å¼åæµç¨

1. å¢å æå¡è¯·æ±è·¯å¾ï¼ä¿®æ¹ **constants/Api.ts** æä»¶

```diff
export const Api = {
+  POST_SERVICE_LIST: `${baseUrl}/service-list/pageSize/:pageSize/page/:page`,
};
```

æç§çº¦å®ï¼è·¯å¾åä»¥å¤§ååè¯·æ±ç±»åå¼å¤´å½å

2. ä¾æ®æ¥å£ææ¡£ï¼ç¼åè¯·æ±æå¡ï¼æ°å»º **services/table-list.service.ts** æä»¶ï¼å¿«æ·é®ï¼tsreqï¼ï¼é¨åä»£ç å¦ä¸ï¼

```ts
import { Api } from 'src/constants/Api';
import request from 'src/utils/request';

export const getServiceList = (
  filter: Omit<ServiceFilter, keyof PageParams>,
  router: PageParams,
) =>
  request<ResponseBody<PageData<Service>>>(Api.POST_SERVICE_LIST, {
    method: 'post',
    router,
    body: JSON.stringify(filter),
  });
```

3. æ°å»º **models/table-list.model.ts** æä»¶ï¼å¿«æ·é®ï¼tsmodelï¼ï¼ç¼åå¯¹åº stateãaction å¤çæ°æ®ååï¼å¹¶å®ä¹å¯¹åºç±»åç¨äºç±»åæ£æ¥ï¼é¨åä»£ç å¦ä¸ï¼

```ts
import { Action, action, ActionTypes, Thunk, thunk } from 'easy-peasy';
import { getServiceList } from 'src/services/table-list.service';

export interface TableListModel {
  data: PageData<Service>;
  filter: ServiceFilter;
  modifyFilter: Action<TableListModel, Partial<ServiceFilter>>;
  resetFilter: Action<TableListModel>;
  setData: Action<TableListModel, PageData<Service>>;
  fetchServiceList: Thunk<TableListModel>;
}

const initState: O.Filter<TableListModel, ActionTypes> = {
  data: {
    list: [],
    total: 0,
  },
  filter: {
    name: '',
    updateDate: '',
    page: 1,
    pageSize: 10,
  },
};

export const tableListModel: TableListModel = {
  ...initState,
  // å¿«æ·é®ï¼act
  modifyFilter: action((state, payload) => {
    state.filter = { ...state.filter, ...payload };
  }),
  resetFilter: action(state => {
    state.filter = initState.filter;
  }),
  setData: action((state, payload) => {
    state.data = payload;
  }),
  // å¿«æ·é®ï¼thunk
  fetchServiceList: thunk(async (actions, payload, { getState }) => {
    const { page, pageSize, ...otherFilter } = getState().filter;
    const res = await getServiceList(otherFilter, { page, pageSize });

    actions.setData(res.data);
  }),
};
```

å¼å¥ modelï¼ä¿®æ¹ **models/index.ts** åå®¹

```diff
+import { tableListModel, TableListModel } from './table-list.model';

export interface StoreModel {
+  tableListModel: TableListModel;
}

export const storeModel: StoreModel = {
+  tableListModel,
};
```

4. ä¸å¡ç»ä»¶ä½¿ç¨ demo

```tsx
import { useStoreActions, useStoreState } from 'src/hooks';

const TableList: React.FC<TableListProps> = props => {
  // å¿«æ·é®ï¼cus
  const {
    data: { total, list },
    filter,
  } = useStoreState(state => state.tableListModel);
  // å¿«æ·é®ï¼cua
  const { setFilter, resetFilter, fetchServiceList } = useStoreActions(
    actions => actions.tableListModel,
  );
  const [state, fetch] = useAsyncFn(() => fetchServiceList());

  useEffect(() => {
    fetch();
  }, [fetch, filter]);

  return (
    <div className={styles.wrap}>
      <div className={styles.header}>
        <Button type="primary">æ¥è¯¢</Button>
        <Button onClick={() => resetFilter()}>éç½®</Button>
      </div>
      <Table
        columns={columns}
        dataSource={list}
        loading={state.loading}
        pagination={{
          total,
          pageSize: filter.pageSize,
          current: filter.page,
          showSizeChanger: true,
          onChange(curr) {
            modifyFilter({ page: curr });
          },
          onShowSizeChange(curr, size) {
            modifyFilter({ page: 1, pageSize: size });
          },
        }}
      />
    </div>
  );
};
```

### å¬å±ä¸å¡ç»ä»¶

å¯¹äºä¸äºå¯è½è¢«å¤å¤å¼ç¨çåè½æ¨¡åï¼å»ºè®®æç¼æå¬å±ä¸å¡ç»ä»¶ç»ä¸ç®¡çãè¿äºç»ä»¶ä¸è¬æä»¥ä¸ç¹å¾ï¼

- åªè´è´£ä¸åç¸å¯¹ç¬ç«ï¼ç¨³å®çåè½
- æ²¡æåç¬çè·¯ç±éç½®
- å¯è½æ¯çº¯éæçï¼ä¹å¯è½åå«èªå·±ç stateï¼ä½ä¸æ¶å redux çæ°æ®æµï¼ä»åç¶ç»ä»¶ï¼éå¸¸æ¯ä¸ä¸ªé¡µé¢ï¼ä¼ éçåæ°æ§å¶

å¦ echart

## å¸å±ä¸è·¯ç±
