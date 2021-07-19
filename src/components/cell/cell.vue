<template>
  <div :class="[_.cell,size && _.large,center && _.center,!border && _.borderless,clickable || isLink && _.clickable,required && _.required]"  v-on="{click: handleClick}">
	
	<slot name="icon"></slot>
	<i v-if="icon && !$slots.icon" :class="[iconFlag==false?iconClassName:'',iconPrefix,_.left_icon]">
		<img :class="[_.image]" v-if="iconFlag" :src="icon">
	</i>
	<div :class="_.title" v-if="title || $slots.title">
		<slot name="title">
			<span>{{title}}</span>
		</slot>
		<div :class="_.label">
			<slot name="label">
				{{label}}
			</slot>
		</div>
	</div>
	<div :class="[_.value,!title && !$slots.title && _.value_alone]">
		<slot name="default">
			<span>{{value}}</span>
		</slot>
	</div>
	<d-icon v-if="isLink" :name="returnValue" :class="[_.right_icon]"/>
	<slot name="right-icon"></slot>
	<slot name="extra"></slot>
  </div>
</template>

<script>
  import { defineComponent } from '@/utils';

  export default defineComponent({
    name: 'Cell',

	data(){
		return{
			iconFlag: false,
			iconClassName: '',
			returnValue:'return'
		}
	},

    props: {
		title: {
			type: String,
			default: '',
			desc: '左侧标题',
		},
		value: {
			type: String,
			default: '',
			desc: '右侧内容',
		},
		label: {
			type: String,
			default: '',
			desc: '标题下方的描述信息',
		},
		size: {
			type: String,
			default: '',
			desc: '单元格大小，可选值为 large',
			enum: ['large'],
		},
		icon: {
			type: String,
			default: '',
			desc: '左侧图标名称或图片链接',
		},
		iconPrefix: {
			type: String,
			default: 'd-icon',
			desc: '图标类名前缀，同 Icon 组件的 class-prefix 属性',
		},
		isLink: {
			type: Boolean,
			default: false,
			desc: '是否展示右侧箭头并开启点击反馈',
		},
		url: {
			type: String,
			default: '',
			desc: '点击后跳转的链接地址',
		},
		to: {
			type: String,
			default: '',
			desc: '点击后跳转的目标路由对象，同 vue-router 的 to 属性',
		},
		border: {
			type: Boolean,
			default: true,
			desc: '是否显示内边框',
		},
		replace: {
			type: Boolean,
			default: false,
			desc: '是否在跳转时替换当前页面历史',
		},
		clickable:{
			type: Boolean,
			default: null,
			desc: '是否开启点击反馈',
		},
		center:{
			type: Boolean,
			default: false,
			desc: '是否使内容垂直居中',
		},
		required:{
			type: Boolean,
			default: false,
			desc: '是否显示表单必填星号',
		},
	},

    emits: {
      click: {
        desc: '点击时触发',
        payload: {
          e: {
            type: Object,
            desc: '事件对象',
          },
        },
      },
    },

    slots: {
      default: {
        desc: '自定义右侧 value 的内容',
      },
	  title: {
        desc: '自定义左侧 title 的内容',
      },
	  label: {
        desc: '自定义标题下方 label 的内容',
      },
	  icon: {
        desc: '自定义左侧图标',
      },
	  'right-icon': {
        desc: '自定义右侧按钮',
      },
	  extra: {
        desc: '自定义单元格最右侧的额外内容',
      },
    },

	created(){
		this.iconFlag = this.icon.indexOf("/") == -1 ? false : true;
		console.log(this.iconFlag);
		this.iconClassName = this.iconPrefix + '-' + this.icon;
	},

    methods:{
        handleClick(e) {
			this.$emit('click', e);
			if(this.to ||this. url){
			this.replace ? (this.to ? this.$router.replace(this.to) : window.location.replace(this.url)) : (this.to ? this.$router
						.push(this.to) : window.location.href = this.url);
			}
				
		}
    }

  });
</script>

<style lang="scss" module>
  .cell {
    position: relative;
	display: -webkit-box;
	display: -webkit-flex;
	display: flex;
	box-sizing: border-box;
	width: 100%;
	padding: 16px 12px;
	overflow: hidden;
	color: #333333;
	font-size: 16px;
	line-height: 25px;
	background-color: #fff;

    .title,.value{
			-webkit-box-flex: 1;
			-webkit-flex: 1;
			flex: 1;
		}

    .value {
			position: relative;
			overflow: hidden;
			color: #999999;
			text-align: right;
			vertical-align: middle;
			word-wrap: break-word;
		}

    .value_alone {
      color: #323233;
      text-align: left;
    }

    &::after {
			position: absolute;
			box-sizing: border-box;
			content: ' ';
			pointer-events: none;
			right: 16px;
			bottom: 0;
			left: 16px;
			border-bottom: 1px solid #E9E9E9;
			-webkit-transform: scaleY(.5);
			transform: scaleY(.5);
		}

    .label {
			margin-top: 6px;
			color: #999999;
			font-size: 13px;
			line-height: 18px;
		}

    &:last-child::after{
      display: none;
    }

	&.borderless::after{
		display: none;
	}

    &.large {
      padding-top: 18px;
      padding-bottom: 18px;
    }

    &.center {
		-webkit-box-align: center;
		-webkit-align-items: center;
		align-items: center;
	}

	&.clickable:active {
	    background-color: #f2f3f5;
	}

	&.required::before {
		position: absolute;
		left: 6px;
		color: #ee0a24;
		font-size: 14px;
		content: '*';
	}

	.image {
		width: 1em;
		height: 1em;
		object-fit: contain;
	}

	.left_icon {
		margin-right: 4px;
	}

	.left_icon, .right_icon {
		height: 28px;
		font-size: 16px;
		line-height: 28px;
	}
	
  }
</style>
 