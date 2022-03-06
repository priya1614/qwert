fun startCountDownTimer() {
        var tick = 60
        addDisposable(Observable.interval(1, TimeUnit.SECONDS)
            .take(61)
            .flatMap {
                return@flatMap Observable.create<Int> { emitter ->
                    emitter.onNext(tick--)
                }
            }
            .subscribeOn(Schedulers.io())
            .observeOn(AndroidSchedulers.mainThread())
            .subscribe({
                timerLiveData.value = it
            }, {})
        )
    }
        
         private fun toggleSwipeTab(show: Boolean) {
        if (isSwipeTabVisible == show)
            return
        if (!show) {
            val h = resources.getDimension(R.dimen._15sdp) + binding.swipeTabView.height
            binding.swipeTabView.animate().withLayer().translationY(h).interpolator =
                AccelerateInterpolator(2f)
        } else
            binding.swipeTabView.animate().withLayer().translationY(0f).interpolator =
                DecelerateInterpolator(2f)
        isSwipeTabVisible = show
    }
        
        
