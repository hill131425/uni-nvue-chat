<template>
	<view>
		<view v-if="loaded || list.itemIndex < 15" class="uni-indexed-list__title-wrapper">
			<text v-if="list.items && list.items.length > 0" class="uni-indexed-list__title">{{ list.key }}</text>
		</view>
		<view v-if="(loaded || list.itemIndex < 15) && list.items && list.items.length > 0" class="uni-indexed-list__list">
			<view class="" v-for="(item, index) in list.items" :key="index">
				<view class="line" v-if="index != 0">
				</view>
				<view class="uni-indexed-list__item" hover-class="uni-indexed-list__item--hover">
					<view class="uni-indexed-list__item-container" :style="androidStyle" @click="onClick(idx, index)">
						<view class="uni-indexed-list__item-border" :class="{'uni-indexed-list__item-border--last':index===list.items.length-1}">
							<view v-if="showSelect" style="margin-right: 20rpx;">
								<uni-icons :type="item.checked ? 'checkbox-filled' : 'circle'" :color="item.checked ? '#04BE02' : '#aaa'" size="48" />
							</view>
							<view class="user" style="display: flex;align-items: center;flex-direction: row;">

								<image :src="$store.state.user.utils.getImageCache(item.name.avatar)" mode="aspectFill" style="width: 80rpx;height: 80rpx;border-radius: 10rpx;margin-right: 10px;"></image>
								<view class="" style="display: flex;flex-direction: column;">
									<text class="uni-indexed-list__item-content">{{ item.name.nickname }}</text>
								</view>
							</view>
						</view>
					</view>
				</view>

			</view>
		</view>
	</view>
</template>

<script>
	import {
		mapState
	} from 'vuex'
	import uniIcons from '../uni-icons/uni-icons.vue'
	export default {
		name: 'UniIndexedList',
		components: {
			uniIcons
		},
		props: {
			loaded: {
				type: Boolean,
				default: false
			},
			idx: {
				type: Number,
				default: 0
			},
			list: {
				type: Object,
				default () {
					return {}
				}
			},
			showSelect: {
				type: Boolean,
				default: false
			}
		},
		computed: {
			...mapState({
				webSocket: state => state.user.webSocket,
			}),
			androidStyle() {
				let style = "";
			 
				if (uni.getSystemInfoSync().platform == "android") {
					style = "margin-left:10px;";
				}
				return "padding:5px;" + style;
			}
		},
		methods: {
			onClick(idx, index) {
				this.$emit("itemClick", {
					idx,
					index
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.uni-indexed-list__list {
		background-color: $uni-bg-color;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		// border-top-style: solid;
		// border-top-width: 1px;
		// border-top-color: $uni-border-color;
	}

	.uni-indexed-list__item {
		font-size: $uni-font-size-lg;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex: 1;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
	}

	.uni-indexed-list__item-container {
		padding-left: $uni-spacing-row-lg;
		flex: 1;
		position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		box-sizing: border-box;
		/* #endif */
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
	}

	.uni-indexed-list__item-border {
		flex: 1;
		position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		box-sizing: border-box;
		/* #endif */
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 100rpx;
		padding: $uni-spacing-row-lg;
		padding-left: 0;
		// border-bottom-style: solid;
		// border-bottom-width: 1px;
		// border-bottom-color: $uni-border-color;
	}

	.uni-indexed-list__item-border--last {
		border-bottom-width: 0px;
	}

	.uni-indexed-list__item-content {
		flex: 1;
		font-size: 34rpx;
		color: black;
		lines: 3;
		width: 500rpx;
		overflow: hidden;
		/* #ifndef APP-NVUE */
		word-wrap: break-word
		/* #endif */
		 
	}

	.line {
		/* #ifndef APP-NVUE */
		align-self: flex-end;
		/* #endif */
		width: 590rpx;
		height: 2rpx;
		background-color: #f3f3f3;
	}

	.uni-indexed-list {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
	}

	.uni-indexed-list__title-wrapper {
		/* #ifndef APP-NVUE */
		display: flex;
		width: 100%;
		/* #endif */
		background-color: #ebebeb;
	}

	.uni-indexed-list__title {
		padding: 12rpx 24rpx;
		line-height: 48rpx;
		font-size: $uni-font-size-sm;
	}

	.slot-box {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		align-items: center;
	}

	.slot-image {
		/* #ifndef APP-NVUE */
		display: block;
		/* #endif */
		margin-right: 20rpx;
		width: 60rpx;
		height: 60rpx;
	}

	.slot-text {
		font-size: 28rpx;
		color: #4cd964;
		margin-right: 20rpx;
	}
</style>
