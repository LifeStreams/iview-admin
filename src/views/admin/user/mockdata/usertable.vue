<script>
export const userTableTitle = [
    {
        title: '账号',
        align: 'center',
        key: 'account',
        editable: true
    },
    {
        title: '姓名',
        align: 'center',
        key: 'userName',
        editable: true
    },
    {
        title: '性别',
        align: 'center',
        key: 'gender'
    },
    {
        title: '邮箱',
        align: 'center',
        key: 'email',
        editable: true
    },
    {
        title: '类型',
        align: 'center',
        key: 'type',
        editable: true
    },
    {
        title: '锁定',
        align: 'center',
        key: 'lock',
        render: (h, params) => {
            return h('i-switch', {
                props: {
                    value: params.row.lock === '1',
                    'true-value': '1',
                    'false-value': '0'
                },
                on: {
                    'on-change': (value) => {
                        this.$Message.success(value);
                    }
                }                
            });
        }
    },
    {
        title: '操作',
        align: 'center',
        width: 200,
        key: 'handle',
        render: (h, params) => {
            return [h('Button', {
                props: {
                    type: 'error',
                    size: 'small'
                },
                style: {
                    marginRight: '3px'
                },
                on: {
                    click: () => {
                        
                    }
                }
            }, '删除'), h('Button', {
                props: {
                    type: 'primary',
                    size: 'small'
                },
                style: {
                    marginRight: '3px'
                },
                on: {
                    click: () => {

                    }
                }
            }, '编辑'), h('Button', {
                props: {
                    type: 'warning',
                    size: 'small'
                },
                on: {
                    click: () => {

                    }
                }
            }, '锁定')];
        }
    }
];
</script>