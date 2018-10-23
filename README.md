<!DOCTYPE HTML>
<html>

<head>
    <title>echarts</title>
    <script type="text/javascript" src="echarts.min.js"></script>
    <script type="text/javascript" src="china.js"></script>
</head>

<body>
    <div id="main" style="width: 1000px;height:700px;"></div>
    <script type="text/javascript">
        var myChart = echarts.init(document.getElementById('main'));



        var data = [{
                name: "上海",
                value: 55.7
            }, {
                name: "海口",
                value: 56
            }, {
                name: "合肥",
                value: 54.4
            }, {
                name: "南京",
                value: 53.6
            }, {
                name: "杭州",
                value: 55.2
            }, {
                name: "广州",
                value: 55.3
            }, {
                name: "福州",
                value: 57.5
            }, {
                name: "南宁",
                value: 56.1
            }, {
                name: "郑州",
                value: 56
            }, {
                name: "武汉",
                value: 56.1
            }, {
                name: "长沙",
                value: 53.3
            }, {
                name: "南昌",
                value: 53.6
            }, {
                name: "北京",
                value: 53.2
            }, {
                name: "长春",
                value: 56.2
            }, {
                name: "沈阳",
                value: 54.8
            }, {
                name: "哈尔滨",
                value: 59.3
            }, {
                name: "天津",
                value: 53.9
            }, {
                name: "济南",
                value: 53.7
            }, {
                name: "太原",
                value: 53.2
            }, {
                name: "石家庄",
                value: 54.4
            }, {
                name: "西安",
                value: 56.5
            }, {
                name: "成都",
                value: 54.3
            }, {
                name: "重庆",
                value: 53.1
            }, {
                name: "昆明",
                value: 53.2
            }, {
                name: "拉萨",
                value: 48.2
            }, {
                name: "银川",
                value: 53
            }, {
                name: "西宁",
                value: 53.8
            }, {
                name: "兰州",
                value: 53.9
            }, {
                name: "呼和浩特",
                value: 54
            }, {
                name: "乌鲁木齐",
                value: 54.4
            }, {
                name: "贵阳",
                value: 58.8
            },


        ];

        var geoCoordMap = {
            "上海": [121.48, 31.22],
            "海口": [110.35, 20.02],
            "合肥": [117.27, 31.86],
            "南京": [118.78, 32.04],
            "杭州": [120.19, 30.26],
            "广州": [113.23, 23.16],
            "福州": [119.3, 26.08],
            "南宁": [108.33, 22.84],
            "郑州": [113.65, 34.76],
            "武汉": [114.31, 30.52],
            "长沙": [113, 28.21],
            "南昌": [115.89, 28.68],
            "北京": [116.46, 39.92],
            "长春": [125.35, 43.88],
            "沈阳": [123.38, 41.8],
            "哈尔滨": [126.63, 45.75],
            "天津": [117.2, 39.13],
            "济南": [117, 36.65],
            "太原": [112.53, 37.87],
            "石家庄": [114.48, 38.03],
            "西安": [108.95, 34.27],
            "成都": [104.06, 30.67],
            "重庆": [106.54, 29.59],
            "昆明": [102.73, 25.04],
            "拉萨": [91.11, 29.97],
            "银川": [106.27, 38.47],
            "西宁": [101.74, 36.56],
            "兰州": [103.73, 36.03],
            "呼和浩特": [111.65, 40.82],
            "乌鲁木齐": [87.68, 43.77],
            "贵阳": [106.71, 26.57],
        };

        var convertData = function(data) {
            var res = [];
            for (var i = 0; i < data.length; i++) {
                var geoCoord = geoCoordMap[data[i].name];
                if (geoCoord) {
                    res.push({
                        name: data[i].name,
                        value: geoCoord.concat(data[i].value)
                    });
                }
            }
            return res;
        };

        var convertedData = [
            convertData(data),
            convertData(data.sort(function(a, b) {
                return b.value - a.value;
            }).slice(0, 6))
        ];
        data.sort(function(a, b) {
            return a.value - b.value;
        })

        var selectedItems = [];
        var categoryData = [];
        var barData = [];
        //   var maxBar = 30;
        var sum = 0;
        var count = data.length;
        for (var i = 0; i < data.length; i++) {
            categoryData.push(data[i].name);
            barData.push(data[i].value);
            sum += data[i].value;
        }
        console.log(categoryData);
        console.log(sum + "   " + count)
        option = {
            backgroundColor: '#404a59',
            animation: true,
            animationDuration: 1000,
            animationEasing: 'cubicInOut',
            animationDurationUpdate: 1000,
            animationEasingUpdate: 'cubicInOut',
            title: [{
                text: '2017年直辖市和省会城市区域声环境质量昼间平均等效声级',
                subtext: 'data from 《2018中国环境噪声污染防治报告》',
                sublink: 'http://dqhj.mee.gov.cn/dqmyyzshjgl/zshjgl/201808/t20180803_447713.shtml',
                left: 'center',
                textStyle: {
                    color: '#fff'
                }
            }, {
                id: 'statistic',
                text: count ? '平均: ' + parseInt((sum / count).toFixed(4)) : '',
                right: 120,
                top: 40,
                width: 100,
                textStyle: {
                    color: '#fff',
                    fontSize: 16
                }
            }],
            toolbox: {
                iconStyle: {
                    normal: {
                        borderColor: '#fff'
                    },
                    emphasis: {
                        borderColor: '#b1e4ff'
                    }
                },
                feature: {
                    dataZoom: {},
                    brush: {
                        type: ['rect', 'polygon', 'clear']
                    },
                    saveAsImage: {
                        show: true
                    }
                }
            },
            brush: {
                outOfBrush: {
                    color: '#abc'
                },
                brushStyle: {
                    borderWidth: 2,
                    color: 'rgba(0,0,0,0.2)',
                    borderColor: 'rgba(0,0,0,0.5)',
                },
                seriesIndex: [0, 1],
                throttleType: 'debounce',
                throttleDelay: 300,
                geoIndex: 0
            },
            geo: {
                map: 'china',
                left: '10',
                right: '35%',
                center: [117.98561551896913, 31.205000490896193],
                zoom: 1.5,
                label: {
                    emphasis: {
                        show: false
                    }
                },
                roam: true,
                itemStyle: {
                    normal: {
                        areaColor: '#323c48',
                        borderColor: '#111'
                    },
                    emphasis: {
                        areaColor: '#2a333d'
                    }
                }
            },
            tooltip: {
                trigger: 'item'
            },
            grid: {
                right: 40,
                top: 100,
                bottom: 40,
                width: '30%'
            },
            xAxis: {
                type: 'value',
                scale: true,
                position: 'top',
                boundaryGap: false,
                splitLine: {
                    show: false
                },
                axisLine: {
                    show: false
                },
                axisTick: {
                    show: false
                },
                axisLabel: {
                    margin: 2,
                    textStyle: {
                        color: '#aaa'
                    }
                },
            },
            yAxis: {
                type: 'category',
                //  name: 'TOP 20',
                nameGap: 16,
                axisLine: {
                    show: true,
                    lineStyle: {
                        color: '#ddd'
                    }
                },
                axisTick: {
                    show: false,
                    lineStyle: {
                        color: '#ddd'
                    }
                },
                axisLabel: {
                    interval: 0,
                    textStyle: {
                        color: '#ddd'
                    }
                },
                data: categoryData
            },
            series: [{
                // name: 'pm2.5',
                type: 'scatter',
                coordinateSystem: 'geo',
                data: convertedData[0],
                symbolSize: function(val) {
                    return Math.max(val[2] / 300, 8);
                },
                label: {
                    normal: {
                        formatter: '{b}',
                        position: 'right',
                        show: false
                    },
                    emphasis: {
                        show: true
                    }
                },
                itemStyle: {
                    normal: {
                        color: '#FF8C00',
                        position: 'right',
                        show: true
                    }
                }
            }, {
                //  name: 'Top 5',
                type: 'effectScatter',
                coordinateSystem: 'geo',
                data: convertedData[0],
                symbolSize: function(val) {
                    return Math.max(val[2] / 500, 8);
                },
                showEffectOn: 'render',
                rippleEffect: {
                    brushType: 'stroke'
                },
                hoverAnimation: true,
                label: {
                    normal: {
                        formatter: '{b}',
                        position: 'right',
                        show: true
                    }
                },
                itemStyle: {
                    normal: {
                        color: '#f4e925',
                        shadowBlur: 50,
                        shadowColor: '#EE0000'
                    }
                },
                zlevel: 1
            }, {
                id: 'bar',
                zlevel: 2,
                type: 'bar',
                symbol: 'none',
                itemStyle: {
                    normal: {
                        color: '#ddb926'
                    }
                },

                data: data
            }]
        };



        function renderBrushed(params) {
            var mainSeries = params.batch[0].selected[0];

            var selectedItems = [];
            var categoryData = [];
            var barData = [];
            var maxBar = 30;
            var sum = 0;
            var count = 0;

            for (var i = 0; i < mainSeries.dataIndex.length; i++) {
                var rawIndex = mainSeries.dataIndex[i];
                var dataItem = convertedData[0][rawIndex];
                var pmValue = dataItem.value[2];

                sum += pmValue;
                count++;

                selectedItems.push(dataItem);
            }

            selectedItems.sort(function(a, b) {
                //   return b.value[2] - a.value[2];
                return a.value - b.value;
            });

            for (var i = 0; i < Math.min(selectedItems.length, maxBar); i++) {
                categoryData.push(selectedItems[i].name);
                barData.push(selectedItems[i].value[2]);
            }

            this.setOption({
                yAxis: {
                    data: categoryData
                },
                xAxis: {
                    axisLabel: {
                        show: !!count
                    }
                },
                title: {
                    id: 'statistic',
                    text: count ? '平均: ' + (sum / count).toFixed(4) : ''
                },
                series: {
                    id: 'bar',
                    //        sort:'descending',
                    data: barData
                }
            });
        }


        myChart.setOption(option);
    </script>
</body>

</html>
