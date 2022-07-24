% File 1
[y,fs] = audioread ('SembilanNmfa.wav') %noisy sample audio
[y1,fs1] = audioread ('SembilanWmfa.wav') %normal sample audio 

info    = audioinfo('SembilanNmfa.wav');
player  = audioplayer(y, fs, info.BitsPerSample);
player.playblocking();

%freq domain
figure;
nfft = 1024;
f = linspace(0,fs,nfft);
Y = abs(fft(y,nfft));
figure (2);
plot(1:nfft,Y(1:nfft));
title('Frequency Domain for Noisy BM 1 Before')
xlabel('Frequency (Hz)')
ylabel('Absolute (dB)')

 
% time domain
t = linspace(0, length(y)/fs, length(y));
t1 = linspace(0, length(y1)/fs1, length(y1));

figure (3);
plot(t,y);
title('Time Domain for Noisy BM 1 Before')
xlabel('Time (s)')
ylabel('Amplitude (dB)')

% Spectogram
figure (4);
% [y,Fs] = audioread('LBM10.wav');
windowSize = 256;
windowOverlap = [];
freqRange = 0:fs;
spectrogram(y(:,1), windowSize, windowOverlap, freqRange, fs, 'xaxis');


% Butterworth Filter
figure(5);
fc = 600;
[ b , a ] = butter ( 6 , fc / ( 1.8*fs / 2 ) ) ;
freqz ( b , a ) ;
filteredSignal = filter ( b , a , y ) ;
player1 = audioplayer ( filteredSignal , fs ) ;
play ( player1 ) ;

% Convert back to normal graph
figure (6);
subplot(2,1,1);
plot(filteredSignal);
title('Time Domain for Noisy BM 1 After')
xlabel('Time (s)')
ylabel('Amplitude (dB)')

f = linspace(0,fs,nfft);
Y = abs(fft(filteredSignal,nfft));
figure(8);
plot(1:nfft,Y(1:nfft));
title('Frequency Domain for Noisy BM 1 After')
xlabel('Frequency (Hz)')
ylabel('Absolute (dB)')

% Time Domain For Expected
figure (7);
subplot(2,1,2);
plot(t1,y1);
title('Time Domain for Expected Result')
xlabel('Time (s)')
ylabel('Amplitude (dB)')

%SNR for the result
figure (8);
f = 3000;
t = 0:1/fs:1; 
x = tanh(sin(2*pi*f*t)+0.1) + 0.001*randn(1,length(t));
periodogram(x,kaiser(length(x),38),[],fs,'power')
snr(x,fs,5);
snr(x,fs,5,'aliased');

%Crosscorelation 
figure (9);
ly1 = length(y1);
ly = length(y);
samples = 1:min(ly1,ly);
subplot(3,1,1), plot (y1(samples));
subplot(3,1,2), plot (y(samples));
[C1, lag1] = xcorr(y1(samples),y(samples));
subplot(3,1,3), plot(lag1/fs,C1);
ylabel("Amplitude"); grid on
title("Cross-correlation ")
