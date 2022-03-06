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
