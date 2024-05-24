program sistema_de_riego_automatico
// Programa para el control automático de riego basado en la humedad del suelo y la distancia del agua

Start
    // Declaración de variables
    Nivel <- 0
    distancia <- 0
    HUMEDAD <- 0

    // Configuración inicial
    call timeanddate.set_date(5, 20, 2024)
    call timeanddate.set24_hour_time(12, 35, 0)
    call datalogger.set_column_titles("HORA", "HUMEDAD", "NIVEL DE AGUA")

    // Función principal para el control del riego
    function on_forever()
        HUMEDAD <- map(call pins.analog_read_pin(AnalogPin.P0), 0, 1023, 0, 100)

        while distancia >= 15 and distancia <= 18 do
            call music.play(music.tone_playable(988, music.beat(BeatFraction.WHOLE)), music.PlaybackMode.UNTIL_DONE)
        end while

        if distancia >= 15 and distancia <= 18 then
            call pins.digital_write_pin(DigitalPin.P12, 0)
        end if

        if HUMEDAD >= 0 and HUMEDAD <= 30 then
            call pins.digital_write_pin(DigitalPin.P12, 1)
            call basic.pause(10000)
            call pins.digital_write_pin(DigitalPin.P12, 0)
        else if HUMEDAD >= 31 and HUMEDAD <= 50 then
            call pins.digital_write_pin(DigitalPin.P12, 1)
            call basic.pause(7000)
            call pins.digital_write_pin(DigitalPin.P12, 0)
        else if HUMEDAD >= 51 and HUMEDAD <= 80 then
            call pins.digital_write_pin(DigitalPin.P12, 1)
            call basic.pause(5000)
            call pins.digital_write_pin(DigitalPin.P12, 0)
        else
            call pins.digital_write_pin(DigitalPin.P12, 0)
            call basic.pause(2000)
        end if

        call basic.pause(5000)
    end function

    repeat forever on_forever

    // Función para medir la distancia y calcular el nivel de agua
    function on_forever2()
        distancia <- call sonar.ping(DigitalPin.P1, DigitalPin.P2, PingUnit.CENTIMETERS)
        Nivel <- map(call sonar.ping(DigitalPin.P1, DigitalPin.P2, PingUnit.CENTIMETERS), 2, 18, 0, 100)
        call basic.pause(1800000)
    end function

    repeat forever on_forever2

    // Función para enviar datos de humedad y distancia por el puerto serial
    function on_forever3()
        call serial.write_number(HUMEDAD)
        call serial.write_string("")
        call serial.write_number(call sonar.ping(DigitalPin.P1, DigitalPin.P2, PingUnit.CENTIMETERS))
        call serial.write_string("")
        call basic.pause(5000)
    end function

    repeat forever on_forever3

    // Función para registrar datos en el datalogger a intervalos regulares
    function on_every_interval()
        call datalogger.log(
            call datalogger.create_cv("HUMEDAD", HUMEDAD),
            call datalogger.create_cv("NIVEL DE AGUA", Nivel),
            call datalogger.create_cv("HORA", call timeanddate.date_time())
        )
    end function

    call loops.every_interval(5000, on_every_interval)

Stop